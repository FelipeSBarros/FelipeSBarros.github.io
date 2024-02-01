---
title: Bug buster
#summary: Entenda o porquê o netCDF é um grande aliado.
tags:
  - Python
  - PT-Br
date: "2022-04-15T00:00:00Z"

# Optional external URL for project (replaces project detail page).
#external_link: https://felipesbarros.github.io/test/post/hacktoberfest-2021/

image:
  caption:
  focal_point: top
---

## Como tudo começou:

Estou trabalhando num projeto onde uma das funções do python é executada e recebe um um parâmtero pelo terminal. Um detalhe é que esse parâmetro é o nome de uma pessoa. Um ponto que não previ no processo de desenvolvimento é que nomes, como qualquer outro elemento textual da lingua portuguesa, podem ter acentos (ou “caracteres especiais”).

Pois é, foi praticamente sem querer que vi, olhando os logs produzidos, que os nomes com acento estavam com problema de `encoding`.

E assim começou a minha caça ao bug. Uma caça que me tomou um dia e meio. Mas foi de grande aprendizado.

### Um pouco do contexto:
Antes de descrever essa aventura, comento um pouco o fluxo do programa que apresentou erro:

1. Uma função é executada pelo terminal e recebe um parâmtero, que é o nome de uma pessoa;
1. Esse nome é usado para instanciar um objeto. Logo no `__init__` tenho o ponto de acesso ao que foi informado pelo terminal com a incorporação do mesmo como atributo da instância.
1. Alguns processamnetos, que não vem ao caso, são realizados;
1. O log do processamento realizado é persistirdo numa base de dados usando o `SQLAlchemy`, onde a tabela que o recebe possui um campo id e outro json, com os logs organizados em tal formato.

## E agora? Por onde começar?

###Buscando o bug no terminal

Como o parâmetro estava sendo passado por terminal, achei que o problema estava nesse ponto: no terminal. Primeiro passo: checar o encoding usado pelo sistema. Mas logo vi que estava tudo em `utf-8`, o que por sí, não deveria apresentar problema.

Como o nome estava sendo passado como um parâmetro do sistema a partir de uma variável, aproveitei para checar se o erro não estava aí. Nada que um print e alguns testes no terminal não resolva. E nada, os nomes armazenados na variáve e passados como parâmetro não sofriam qualquer alteração neste processo inicial.

### Interseção terminal/python

Achei, então que o erro estava em alguma incompatibilidade entre o que era passado no terminal e o como o python estava recebendo.

Segundo passo, então, foi checar o ponto de contato entre terminal e o python. Ler o seguinte trecho, de uma resposta do stackOverFlow me deu a certeza de que era aí o erro:

> When Python does not detect that it is printing to a terminal, sys.stdout.encoding is set to None.

Ou seja, quando o python não pode detectar o que está sendo apresentado ao terminal o `sys.stdout.encoding` é definido como `None`; Ora, estou passando um parametro a partir de uma variável do terminal, logo um string. O Python não consegue identificar o encoding dessa string e está definindo, então o encoding a None, o que deve estar gerando o erro.

Tentando resolver isso, busquei alguma forma de declarar o encoding… Cheguei a adicionar ao `__init__`, quando a classe é instanciada e recebe o nome da pessoa os métodos, `.encode().decode('utf-8')` ao objeto que recebe o valor. Parecia que ia funcionar, vejam:

```python
nome = 'Felipe Sodré'
b'Felipe Sodr\xc3\xa9'
# e ao adicionar o decode o texto volta ao normal...
nome.encode().decode('utf-8')
'Felipe Sodré'
```

“Meio” gambiarra, não? Mas o importante é se funcionar.

Contudo, o que parecia a solução, foi logo por agua abaixo na primeira rodada de teste. O nome continua com erro de encoding.

Decidí, então, usar o módulo `logging` para apresentar o nome recebido pelo terminal e nome após a classe estar instanciada durante o processamento. Aliás, o [@dunosauro](https://twitter.com/dunossauro) apresentou uma [live muito boa sobre o uso do `logging`](https://www.youtube.com/watch?v=PGAOqAWuwC0)…

Bom, ao usar o `logging` tive certeza de que estava tentando resolver o erro no ponto errado, todas as mensagens de log estavam sem o tal erro de encoding, mas no log persistido no banco de dados seguia com o maldito erro…

Será que o banco de dados está configurado com uma encoding diferente?

### No banco de dados…

✔️ Banco configurado como ‘utf-8’;

Até que me veio uma luz: nas mensagens de log o nome está sem erro. Mas o log que está sendo persistido no banco de dados ( que são algumas dessas mensagens filtradas para monitorar alguns pontos importantes do sistema) é uma compilação salva em um campo JSON.

“Bom deve ser nesse ponto, então.”, pensei.

### Reproduzindo o erro em `JSON`

Parti então para tentar reproduzir esse erro:

```python
>>>import json
>>>info = {'nome':'Felipe Sodré', 'idade':38}
>>>info
{'nome': 'Felipe Sodré', 'idade': 28}
>>>json.dumps(info)
'{"nome": "Felipe Sodr\xc3\xa9", "idade": 38}'
```

Pronto! Aí está o problema. No processo de conversão do dicionário ao JSON, há algum tipo de conversão que gera o erro de encoding.

Não levei “muito tempo” (tempo é relativo, né?) para encontrar que o método [`dumps()`](https://docs.python.org/3/library/json.html#json.dumps) possui o parâmetro `ensure_ascii`, com valor padrão `True`, que garante que as `strings` do JSON que possuam caracteres não-ASCII estejam com scape.:

> If ensure_ascii is true (the default), the output is guaranteed to have all incoming non-ASCII characters escaped. If ensure_ascii is false, these characters will be output as-is.

Testei usando o dumps() com ensur_ascii=False:

```python
>>>json.dumps(info, ensure_ascii=False)
'{"nome": "Flávia Duarte Nascimento", "idade": 12}'
```

Pronto, ponto de erro encontrado. Basta adicionar o parâmetro apra False e tudo se resolveria.

Mas não foi bem assim, ainda faltava um ponto. Eu não estava gerando o dump e salvando no banco. O que estou fazendo é passar o dado, ainda em dicionário, para o banco usando o SQLAlchemy e ele cuida disso para mim.

Como, ou melhor, onde, então, eu devo informar esse `ensure_ascii`?

## Enfim, a solução:

Foi lendo [essa responta no SOF](https://stackoverflow.com/a/36438671) que entendí que como o ORM SQLAlchemy está cuidadno disso para mim, ele possui um serializador e que o mesmo é, nada mais, nada menos que os métodos `json.dumps()` e `json.loads()`, passados na função `create_engine` como um kwargs:

```python
engine = create_engine(..., json_serializer=dumps)
```

O golpe final foi ao ler a docuementação do SQLAlchemy sobre [o tipo de dado JSON](https://docs.sqlalchemy.org/en/14/core/type_basics.html#sqlalchemy.types.JSON) e aprender que podemos customizar o serializador. Olha só o exemplo da documentação, me dando de “bandeja” a solução para o bug em questão:

```python
engine = create_engine(
    "sqlite://",
    json_serializer=lambda obj: json.dumps(obj, ensure_ascii=False))
```

Agora sim, vida que segue, graças à persistẽncia e perseverança na caça aos bugs.

Ah, claro. Essa investigação contou com a ajuda de outros colegas que dedicaram alguns minutos para conversar e propor soluções, tabém. Muito obrigado!

## Atualização

Quando achei que estava tudo funcionando e coloquei em produção a correção, eis que me deparo com um novo erro. Dessa vez um `TypeError`:

```python
raise TypeError(f'Object of type {o.__class__.__name__} '
sqlalchemy.exc.StatementError: (builtins.TypeError) Object of type datetime is not JSON serializable
```

Com algumas pesquisas, pude identificar que, como estou indicando um serializador, Todo objeto a ser inluido no JSON passará por ele. Mas, como o próprio erro informa, um objeto `datetime` não pode ser seriaizado. E por isso que o método `json.dumps()`, além de ter o parâmetro `ensure_ascii`, possui um argumento para a serialização padrão.

Portanto o último bug foi resolvido usando o parâmetro `default=str`. Ou seja, o serializador padrãoa pe transformar o objeto a uma classe string.

O codigo ficou, então da seguinte forma:

```
engine = create_engine(
    "sqlite://",
    json_serializer=lambda obj: json.dumps(obj, ensure_ascii=False, default=str))
```

E vocês, que estratégias adotam na caça aos bugs?

Note: image from [@ThePracticalDev](https://www.mclibre.org/consultar/documentacion/listados/thepracticaldev.html)

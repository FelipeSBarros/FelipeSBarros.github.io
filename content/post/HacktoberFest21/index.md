---
title: "Hacktoberfest: Colaborações e aprendizados."
#summary: Criando um sistema para gestão de dados geográficos de forma simples e robusta Artigo publicado também no linkedin. Este ano pude participar do projeto de jornalismo de dados Engolindo Fumaça, desenvolvido pelo InfoAmazonia.
tags:
  - Python
  - PT-Br
date: "2021-05-21T00:00:00Z"

# Optional external URL for project (replaces project detail page).
#external_link: https://felipesbarros.github.io/test/post/hacktoberfest-2021/

image:
  caption:
  focal_point: smart
---

*Artigo publicado também no [linkedin](https://www.linkedin.com/pulse/hacktoberfest-colabora%C3%A7%C3%B5es-e-aprendizados-felipe-sodr%C3%A9-mendes-barros/).*

O [HacktoberFest](https://hacktoberfest.digitalocean.com/) é um evento promovido pela Digital Ocean durante o mês de outubro e já está na sua oitava edição. O objetivo é incentivar a colaboração em projetos de código aberto e, claro, como uma forma de democratizar o conhecimento em sistemas de versionamento, como o [git](https://git-scm.com/), além de outras tecnologias.

> …Ah, e o incentivo vem com a possibilidade de ganhar uma camisa do evento ao ter aprovado quatro [pull requests](https://git-scm.com/docs/git-request-pull) em repositórios participantes (para participar, basta adicionar a tag “Hactoberfest” ao repositório ou adicionar a tag “Hacktoberfest-accepted” no Pull request em questão).

Não foi minha primeira participação, mas foi a primeira vez que pude colaborar em projetos diferentes daqueles relacionados ao meu trabalho cotidiano. E já fazia algum tempo que tinha interesse em colaborar, mas não sabia como quebrar a inércia. Compartilho neste artigo, alguns projetos desenvolvidos este ano e o que pude aprender nos mesmos.

## Fogo Cruzado

O projeto [Fogo Cruzado](https://fogocruzado.org.br/) foi desenvolvido pela [Volt Data Lab](https://voltdata.info/) e [Instituto Fogo Cruzado](https://twitter.com/fogocruzado), como um sistema [Crowdsourcing](https://pt.wikipedia.org/wiki/Crowdsourcing) para monitoramento dos tiroteios no Rio de Janeiro e/ou em Recife. O mesmo [disponibiliza uma API](https://fogocruzado.org.br/sobre-a-api/) para acessar aos dados, bastando criar um usuário, sem custo. E o projeto já tem um pacote para acessar os dados pelo [R](https://github.com/voltdatalab/crossfire).

Como faltava um módulo python para acessar os dados do projeto, decidi fazê-lo durante o #Hacktoberfest. Esse foi o primeiro projeto: um módulo python para acessar os dados da API, direto do python.

Foi um desafio legal e, até certa forma, simples, pois eu já tinha um modelo de como funcionava o pacote em R. Então o trabalho foi, principalmente “traduzir” ao python. Com isso aproveitei para refatorar algumas partes do código.

No geral, posso dizer que ao desenvolver esse projeto, aprendi sobre:

* Python-poetry (do zero);
* Validação de login usando variáveis do sistema;
* Publicação de módulos no PyPi;

### E fica como desafios para melhor/implementar em breve:

* Melhorar o código com `type annotation`;
* Criação de documentação com `Sphynx` (se alguém quiser sugerir outra alternativa será bem-vinda);

## PyInaturalist-convert

![](pyinaturalist_logo_med.png)

O segundo projeto que atuei nesse mês foi no [PyInaturalist-convert](https://github.com/JWCook/pyinaturalist-convert). A história deste módulo é bem interessante e surge de uma demanda pessoal: O [IMiBio](https://imibio.misiones.gob.ar/), Instituição onde trabalho, está desenvolvendo um projeto com o [INaturalist](https://www.inaturalist.org/), uma aplicação de [crowdsourcing](https://pt.wikipedia.org/wiki/Crowdsourcing) para observação de biodiversidade, e eu tive que criar um sistema que acesse os dados do projeto usando a [API deles](https://github.com/inaturalist/iNaturalistAPI). Com isso, conheci o módulo [PyINaturalist](https://github.com/niconoe/pyinaturalist). Conversando com os desenvolvedores, comentei que seria interessante ter os dados no padrão [darwincore](https://dwc.tdwg.org/). Um deles achou pertinente e começamos a desenvolver juntos. Contudo, fiquei uns bons meses afastado do projeto e ao voltar, já era um pacote bem estruturado. Por isso, para entender a estrutura do mesmo e saber por onde começar, além de ler as [issues](https://guides.github.com/features/issues/) abertas, adotei a estratégia de ler os testes…

… E foi lendo os testes que percebi que estavam implementando um objeto `geojson`, “na unha”. Como estive estudando sobre o `geojson` (e, inclusive foi um dos temas explorados por mim em [outros artigos](https://felipesbarros.github.io/post/criando-um-sistema-para-gestao-de-dados-geograficos-de-forma-simples-e-robusta-ii/), propus usá-lo. Com isso, poderíamos usar os métodos de validação já implementados no módulo, garantindo consistência aos dados;

Ao colaborar no módulo `PyInaturalist-converter`, aprendi sobre:

* Como colaborar a um projeto já estruturado. Tenho certeza que essa não é uma regra. Mas foi uma boa estratégia começar lendo os testes;
* Mais aprendizados sobre python-poetry :);
* Soube da existência do formatador de código `Black`;
* Soube da existencia do [ISORT](https://pycqa.github.io/isort/), para padronizar os `imports`;

Além desses aprendizados, o autor principal do módulo já tinha configurado no repositório um [fluxo de ações](https://docs.github.com/pt/actions) e validações bem interessantes. Dessa forma, havia um sistema de validação do que se estava propondo como `pull request`. Ainda não tive tempo de me aprofundar, mas já está na lista de estudos futuros…

## Análise espacial no frontend

Uma última atividade que queria compartilhar, não está relacionada a uma contribuição minha, mas sim, um projeto ao qual eu recebi ajuda.

[Publiquei recentemente](https://www.linkedin.com/pulse/an%C3%A1lise-espacial-frontend-felipe-sodr%C3%A9-mendes-barros?trk=public_post-content_share-article) um artigo apresentando alguns módulos de JavaScript que nos permitem fazer algumas análises espaciais sem depender de uma infraestrutura de servidores de dados e de mapas.

Eu fui apresentado a essas tecnologias no [FOSS4G 2021](https://2021.foss4g.org/) e por pura curiosidade, já que frontend não é a “minha praia”, comecei a fazer alguns testes como estratégia de estudos, mesmo.

Pude evoluir bastante com os estudos, mas num momento vi que poderia ser feito muito mais, mas que eu não tinha conhecimento técnico em JS para isso. Não tive dúvidas em contactar um amigo que trabalha com JS e apresentei a ele o que estava tentando fazer. Ele curtiu e acabou colaborando com o projeto, transformando essa prova de conceito numa solução, em algo realmente interessante.

Percebam que essa colaboração não surgiu pelo Hacktoberfest. Mas por uma mudança de postura minha em me conectar com outras pessoas e apresentar o que eu estava estudando, as “minhas dores” e o que pretendia fazer.

Neste projeto estudei e aprendi sobre:

* O `georaster`, uma biblioteca JavaScript que nos permite carrregar, e até mesmo criar, dados raster a partir de objetos JavaScript;
* `georaster-layer-for-leaflet` que é uma biblioteca que nos permite apresentar dados `raster` (a princípio geotif) nos mapas feitos em `leaflet`;
* `geoblaze` que é um pacote desenvolvido em JavaScript para permitir analisar dados carregados como georaster.

Como resultado, criamos dois visualizadores de dados raster apenas com tecnologia frontend. [No primeiro o usuário interage com o pixel](https://felipesbarros.github.io/geoblaze_test/clicking_pixel) (clicando num píxel específico) e o gráfico apresenta o comportamento temporal daquele pixel; [No segundo visualizador o usuário clica em um dos estados](https://felipesbarros.github.io/geoblaze_test/clicking_polygon) e o gráfico apresenta o valor médio dos pixels daquele estado ao longo do tempo.

## Notas finais sobre Hacktoberfest

Entendo que muitos “torcem o nariz” para o Hacktoberfest, pois poucos o utilizam como uma estratégia de estudos, crescimento ou colaboração a projeto de código aberto, que são os objetivos principais. A ideia de escrever sobre as colaborações feitas é justamente destacar que o evento é uma grande estratégia/ferramenta para aprender mais, conectar-se com outros desenvolvedores e se engajar em projetos de código aberto.

Espero que os meus aprendizados serviam de motivação aos demais. Qualquer coisa, fico à disposição para conversar mais a respeito.

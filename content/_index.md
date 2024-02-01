---
# Leave the homepage title empty to use the site title
title: ''
date: 2022-10-24
type: landing

sections:
  - block: about.biography
    id: about
    content:
      title: About me
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
  - block: skills
    content:
      title: Skills
      text: ''
      # Choose a user to display skills from (a folder name within `content/authors/`)
      username: admin
    design:
      columns: '1'
  - block: accomplishments
    id: awards
    content:
      title: 'Awards'
      subtitle:
      date_format: Jan 2006
      # Accomplishments.
      #   Add/remove as many `item` blocks below as you like.
      #   `title`, `organization`, and `date_start` are the required parameters.
      #   Leave other parameters empty if not required.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - date_end: ''
          date_start: '2024-01-31'
          description: 'Anthem Awards Bronze recognition on category "News & Journalism" with the project [Engolindo Fumaça](https://infoamazonia.org/project/engolindo-fumaca/)'
          icon:
          organization: 'Anthem Awards'
          organization_url: https://www.anthemawards.com/
          title: 'Anthem Awards Bronze recognition'
          url: 'https://www.anthemawards.com/winners/list/entry/#health/awareness-media-categories/inhaling-smoke-engolindo-fumaa/457279'

        - date_end: ''
          date_start: '2022-06-01'
          description: 'Winner of the “Rey de España” award in environmental category with the project [Engolindo Fumaça](https://infoamazonia.org/project/engolindo-fumaca/)'
          icon:
          organization: 'Agencia Española de Cooperación Internacional para el Desarrollo (Aecid) y la Agencia EFE'
          organization_url: https://agenciaefe.es/premios-rey-espana/
          title: 'Winner of the “Rey de España” award in environmental category'
          url: 'https://agenciaefe.es/premios-rey-espana/'

        - date_end: ''
          date_start: '2021-11-01'
          description: 'Unanimously nominated by the jury, winner of the Claudio Weber Abramo Award for Data Journalism with the project [Engolindo Fumaça](https://infoamazonia.org/project/engolindo-fumaca/)'
          icon:
          organization: 'Conferência de Jornalismo de Dados e Métodos Digitais (Coda.Br)'
          organization_url: https://escoladedados.org/coda2021/premio-claudio-weber-abramo-de-jornalismo-de-dados/
          title: '1° 1st place in the Claudio Weber Abramo Award for Data Journalism'
          url: 'https://escoladedados.org/coda2021/premio-claudio-weber-abramo-de-jornalismo-de-dados/'
          
        - date_end: ''
          date_start: '2021-06-01'
          description: '2nd place in the MapBiomas Award in the General Category with the article [Achieving cost-effective landscape-scale forest restoration through targeted natural regeneration](https://conbio.onlinelibrary.wiley.com/doi/10.1111/conl.12709)'
          icon:
          organization: 'MapBiomas Brazil'
          organization_url: https://mapbiomas.org/premio
          title: '2nd place in the MapBiomas Award'
          url: 'https://mapbiomas.org/premio'
          
        - date_end: ''
          date_start: '2017-09-01'
          description: '3rd place in Hackathon Industry 4.0 held in the city of Posadas, Misiones - Argentina. On this occasion, I worked with the [colmena](http://proyectocolmenar.org/noticias/presentacion-proyecto-colmena-en-camara/itemlist/tag/FuDeCo) group to develop a Minimum Viable Product.'
          icon:
          organization: 'Ministry of Industry'
          organization_url: https://industria.misiones.gob.ar/es/
          title: '3rd place in Hackathon Industry 4.0'
          url: 'https://www.industria.misiones.gob.ar/es/noticias/noticias/415-se-realizara-el-reto-industria-4-0-el-primer-hackaton-en-misiones-para-la-industria'
          
        - date_end: ''
          date_start: '2017-05-01'
          description: '1st place in the Citizen Innovation Hackathon held in the city of Posadas, Misiones - Argentina. In this event, a prototype of a decision-making aid system was developed based on open geographic data using geomarketing concepts.'
          icon:
          organization: 'City of Posadas'
          organization_url: https://www.hackathon.com/event/hackathon-posadas-de-innovacion-ciudadana-34681044939
          title: '1st place in the Citizen Innovation Hackathon'
          url: 'http://ampmnoticias.com/index.php/mas-de-170-personas-participaron-de-la-primera-hackathon/'
          
        - date_end: ''
          date_start: '2014-10-01'
          description: 'Jabuti Literature Award in the Natural Sciences category with Brazilian’s flora Red Book, coordinated by Gustavo Martinelli and Miguel Avila Moraes.'
          icon:
          organization: 'Jabuti Award'
          organization_url: https://www.premiojabuti.com.br/
          title: 'Jabuti Literature Award in the Natural Sciences category'
          url: 'http://jbrj.gov.br/node/322'
          
    design:
      columns: '2'

  - block: portfolio
    id: projects
    content:
      title: Projects
      filters:
        folders:
          - project
      # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
      default_button_index: 0
      # Filter toolbar (optional).
      # Add or remove as many filters (`filter_button` instances) as you like.
      # To show all items, set `tag` to "*".
      # To filter by a specific tag, set `tag` to an existing tag name.
      # To remove the toolbar, delete the entire `filter_button` block.
      buttons:
        - name: All
          tag: '*'
        - name: Python
          tag: Python
        - name: R
          tag: R
    design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
      columns: '3'
      view: card
      # For Showcase view, flip alternate rows?
      flip_alt_rows: false
      
  - block: experience
    id: experience
    content:
      title: Professional experience
      # Date format for experience
      #   Refer to https://docs.hugoblox.com/customization/#date-format
      date_format: Jan 2006
      # Experiences.
      #   Add/remove as many `experience` items below as you like.
      #   Required fields are `title`, `company`, and `date_start`.
      #   Leave `date_end` empty if it's your current employer.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - title: Professor
          company: Faculty Forest Sciences @ National University of Misiones
          company_url: 'https://www.facfor.unam.edu.ar/'
          company_logo:
          location: Eldorado, Misiones - Argentina
          date_start: '2022-01-01'
          date_end: ''
          description: |2-
              Responsibilities:

              - Physical Geography
              - Digital Image Processing
              - GIS III (Geographic Information Systems)
        
        - title: Geographic data scientist
          company: Instituto Misionero de Biodiversidad - IMiBio
          company_url: 'https://felipesbarros.github.io/www.imibio.misiones.gob.ar'
          company_logo:
          location: Posadas, Misiones - Argentina
          date_start: '2020-01-01'
          date_end: '2022-11-01'
          description: |2-
              Specialist responsible for the Institute’s space and environmental solutions. Responsabilidades:

              * Desenvolvimento de sistema de análise de dados (Django)
              * Remote Sensing (GEE) and GIS (R & Python) data analysis
              * Scientific writing
            
        - title: Web scrapping developer
          company: Volt Data Lab
          company_url: 'https://voltdata.info/'
          company_logo:
          location: São Paulo - Brasil
          date_start: '2022-01-01'
          date_end: '2022-12-31'
          description: |2-
              Web scrapping developer responsible creating and maintaining web crawlers using scrapy python framework and spidermon for monitoring the web scrapping process;
              
              Tools and framework used:
            
              * PostgreSQL (SQLAlchemy);
              * scrapy;
              * spaCy (NLP framework);
            
        - title: External consultant
          company: Instituto Internacional para a Sustentabilidade - IIS (Austrália)
          company_url: 'http://www.iis-rio.org/'
          company_logo:
          location: Austrália / Brasil
          date_start: '2017-01-01'
          date_end: '2020-06-01'
          description: |2-
              Responsibilities:

              * Spatial model for forest restoration;
              * Spatial analysis;
              * Scientific writing;
            
        - title: External consultant
          company: International Union for Conservation of Nature - IUCN
          company_url: 'http://www.iucn.org/'
          company_logo:
          location: Austrália / Brasil
          date_start: '2016-11-01'
          date_end: '2017-01-01'
          description: |2-
              Responsibilities:

              * Spearheaded the consolidation and implementation of the Brazilian biodiversity geographic database.
              * Conducted spatial prioritization modeling for the GEF project, defining priority areas for species conservation;
            
        - title: For more details on my previous experiences, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/felipesodre/).
          date_start: '2010-11-01'
          date_end: '2016-01-01'

    design:
      columns: '2'

  - block: accomplishments
    content:
      # Note: `&shy;` is used to add a 'soft' hyphen in a long heading.
      title: 'Accomplish&shy;ments'
      subtitle:
      # Date format: https://docs.hugoblox.com/customization/#date-format
      date_format: Jan 2006
      # Accomplishments.
      #   Add/remove as many `item` blocks below as you like.
      #   `title`, `organization`, and `date_start` are the required parameters.
      #   Leave other parameters empty if not required.
      #   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
      items:
        - certificate_url: https://www.coursera.org
          date_end: ''
          date_start: '2021-01-25'
          description: ''
          icon: coursera
          organization: Coursera
          organization_url: https://www.coursera.org
          title: Neural Networks and Deep Learning
          url: ''

  - block: portfolio
    id: posts
    content:
      title: Recent Posts
      subtitle: ''
      text: ''
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
        folders:
          - post
#        author: ""
#        category: ""
#        tag: ""
#        exclude_featured: false
#        exclude_future: false
#        exclude_past: false
#        publication_type: ""
      default_button_index: 0
      buttons:
        - name: All
          tag: '*'
        - name: Python
          tag: Python
        - name: R
          tag: R
        - name: JS
          tag: JS
        - name: PT-Br
          tag: PT-Br
      design:
      # Choose how many columns the section has. Valid values: '1' or '2'.
        columns: '3'
        view: card
      # For Showcase view, flip alternate rows?
        flip_alt_rows: false
      # Choose how many pages you would like to offset by
#      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: card
      columns: '2'
---

# KIBANA

## C'est quoi
    # Kibana est un client pour ElasticSearch , fournis une interface graphique (UI) accesssible par un navigateur web.    
    # Kibana permet:
        - De recherches des documents
        - De visualiser des documents
        - D'agréger des résultats dans des graphes et des diagrammes.

## Site officiel
    # https://artifacts.elastic.co

## Installation
    # curl https://artifacts.elastic.co/downloads/kibana/kibana-6.5.4-amd64.deb
    # sudo dpkg -i kibana-6.5.4-amd64.deb
    
    
## Start
    # sudo service kibana start
        
## Stop
    # sudo service kibana stop
    
## Requettes
    # Le format des requêtes doit respecter la syntaxe du "mini langage" de requête décrit dans la documentation officielle: 
        https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html
        
        Sélectionner un ou plusieurs champs,dans "Available Fields", sélectionnez un champ, puis "Add".
    
    # john: documents contenant "John" (insensible à la casse) dans un des champs.
    
    # fields.actors:"Harrison Ford": documents dont le champfields.actorscontient "Harrison Ford".
    
    # fields.actors:"Harrison Ford" AND fields.rating:>=8: documents de la recherche précédente et dont la note est supérieure ou égale à 8.
    
    # fields.release_date:[2001 TO 2100]: films sortis au XXIème siècle.
    
    # fields.actors:malkovitch~: films dont un acteur a un nom ressemblant à "malkovitch".
    

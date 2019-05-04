# ELASTICSEARCH

## C'est quoi
    # Elasticsearch est une base de données NoSQL.
    # Elasticsearch est un moteur de recherche capable de stocker une grande quantité de documents et que l'on peut interroger en temps réel.
    # Elasticsearch est moteur de texte distribué.
    # Elasticsearch utilse lucene (moteur de recherche d'appache)

## Site officiel
    # https://www.elastic.co/fr/

## Tutorial en français
    # https://openclassrooms.com/fr/courses/4462426-maitrisez-les-bases-de-donnees-nosql/4474691-etudiez-le-fonctionnement-d-elasticsearch
    # documentations : https://www.elastic.co/guide/en/elasticsearch/reference/current/search.html

## Installation
    # Téléchargement : https://www.elastic.co/fr/downloads
    1- wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.x.x.deb
    2- dpkg -i elasticsearch-6.x.x.deb
   
## Start
    # sudo service elasticsearch start    
    # Test : http://localhost:9200/_cat/health?v

## Stop
    # sudo service elasticsearch stop

## Importation des données
    # Pour importer le fichier json, il faut utiliser le paramètre « data-binary » sur le service REST : _bulk
    # cd PATH_TO_JSON_FILE
    # curl -XPUT -H "Content-Type: application/json" localhost:9200/_bulk --data-binary @movies_elastic.json
    # Test : http://localhost:9200/movies/movie/_search.

## Changer le mapping d'un index
    # curl -XPUT -H "Content-Type: application/json" localhost:9200/movies2 -d @mapping_movies/mapping.json
    # Test : http://localhost:9200/movies2/?pretty
    # ?pretty: pour le rendu au format json
    
## Importer les données du nouveau maping
    # curl -XPUT -H "Content-Type: application/json" localhost:9200/_bulk --data-binary @mapping_movies/movies_elastic2.json  
    # Test : http://localhost:9200/movies2/movie/_search?pretty

## service _search

### API REST -> URL simple
    # http://<host>:<port>/<index>/_search?q=<CRITERS>
    > https://localhost:92000/movies2/_search?q=star Wars
      
    # http://<host>:<port>/<index>/_search?q=<key>:<value>
    > http://localhost:9200/movies2/_search?q=fields.title:Star Wars
    
    # AND : http://<host>:<port>/<index>/_search?q=<key1>:<value1> AND <key2>:<value2>
    > http://localhost:9200/movies2/_search?q=fields.title:Star Wars AND fields.directors:George Lucas
    
    # OR : http://<host>:<port>/<index>/_search?q=<<key1>:<value1> OR <key2>:<value2>
    > http://localhost:9200/movies2/_search?q=fields.title:Star Wars OR fields.directors:George Lucas
    
    # negation (-) : http://<host>:<port>/<index>/_search?q=<-<key>:<value>    
    > http://localhost:9200/movies2/_search?q=actors=Harrison Ford AND fields.plot:Jones AND -fields.plot:Nazis
  
### Requete classic
    # {"query":{"<function>":{"<key>":"<value>"}}}
    
    # MATCH : {"query":{"match":{"<key>":"<value>"}}}
    > {"query":{"match":{"fields.title":"Star Wars"}}}
    
    # MATCH_PHRASE : {"query":{"match_phrase":{"<key>":"<value>"}}}
    > {"query":{"match_phrase":{"fields.title":"Star Wars"}}}
    
    # MUST :  {"query":{"must":{"<key>":"<value>"}}}
    > {"query:"{"must":{"fields.title":"Star Wars"}}}
    
    # SHOULD : {"query":{"bool":{"should":[{"<function>":{"<key>":"<value>"}}]}}}
     {"query":{
        "bool":{
            "should":[
                {"match":{"fields.title":"Star Wars"}},
                {"must":{"fields.directors": "George Lucas"}}
            ]
     }}}
        
     {"query":{
         "bool": {
             "should": [
                 {"match": {"fields.actors": "Harrison Ford"}},
                 {"match": {"fields.plot": "Jones"}}
             ],
             "must_not":{"match":{"fields.plot":"Nazis"}}
     }}}
     
     # RANGE : {"query":{"range":{"<OPERANDE>:"<VALUE>"}}} ; (OPERANDE: lt, lte, gt, gte)
     
     {"query":{
         "bool":{
                 "should":[
                     {"match":{"fields.directors": "James Cameron"}},
                     {"range":{"fields.rank":{"lt":1000}}}
                ]
     }}}
     
     {"query":{
         "bool":{
             "must":[
                 {"match":{"fields.directors": "James Cameron"}},
                 {"range":{"fields.rank": {"lt":1000}}}
             ]
     }}}
     
     {"query":{
         "bool":{
             "must":[
                 {"match_phrase":{"fields.directors": "James Cameron"}},
                 {"range":{"fields.rank": {"lt":1000 }}}
             ]
     }}}
     
     # FILTER
     {"query":{
             "bool":{
                 "must": {"match": {"fields.directors": "J.J. Abrams"}},
                 "filter": {"range": {"fields.release_date":
                     { "from": "2010-01-01", "to": "2015-12-31"}}}
     }}}
    
## Executer une requete en ligne de commande avec curl
        1- sauvegareder la requete dans un fichier <FILE_NAME>
        2- curl -XGET -H "Content-Type: application/json" 'localhost:9200/movies2/movie/_search?pretty' -d @FILE_NAME
        
        > curl -XGET -H "Content-Type: application/json" 'localhost:9200/movies2/movie/_search?pretty' -d @query1


## Etat de santé
    # Cluster : http://localhost:9200/_cluster/health?pretty
    
    # Shards : http://localhost:9200/_cat/shards?pretty
    
    # noeud : ???
    
## Remarques:
    #il n’est pas possible de modifier le mapping d’un index une fois qu’il a été instancié (après la première importation). Il faut soit le supprimer, soit en créer un nouveau
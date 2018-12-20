# MONGODB

## C'est-quoi

    MongoDB est système de getsion de base de données orienté documents, répartissable sur un nembre quelconque d'ordinateur.
    MongoDB ne nécessite pas de schéma prédéfini des données.
    MongoDB est écrit en c++
    MongoDB fait partie de la mouvance NoSQL.
    L'objectif est de pouvoir gérer de grandes quantités de données.
    

## Installation

    Téléchargement : http://www.mongodb.org/downloads
    Suivre la documentation selon l'OS
    mongod : lance le moteur mongodb
    mongo : interpreteur de commande 

## Start service

    $MONGODB_HOME/bin/mongod

## Stop service

    $ sudo service mongodb stop
    
## Création de base de données

    Mongodb ne fourni pas de commande pour créer une base de données.
    Pas besoin de créér manuellement.
    La base est créee lors de la première savegarde de la valeur dans la collection définie. 

## Importation de données

    $MONGO_HOME/bin/mongoimport --db new_data_base --collection new_collections $PATH_TO_FILE/import_file.json

#### Example

    $MONGO/bin/mongoimport --db new_york --collection restaurants $RESTAURANT/restaurants.json


## Format des données

    Le format JSON (JavaScript Object Notation ) est utilisé pour l'insertion et la restitution des documents.
    

## Commandes

### Afficher la liste des bases de données

    >show dbs
    
### Sélectionner une base de donnée

    use DATABASE_NAME
    
    > use cinemadb

### Ajouter un document->  insert | save


    use DATABASE_NAME
    db.<COLLECTION_NAME>.insert({<document>)
    
    >use cinemadb
    >db.actors.insert({"name": "Dupond", "lastname":"Martin"})

### Ajouter une clé  dans un document -> $set

### Supprimer un document -> remove

### Supprimer une clé  d'un document -> $unset

## Mise à jour  d'un document -> update

## Mise à jour multiple -> $multi:true

### Rechercher 

#### find

#### distinct

#### filtrage

#### projection


## Remarques
    
    Une base de données mongo contient des collections dans lequelles des documents sont ajoutés.
    Une collection est un ensemble de documents de me nature.
    MongoDB limite la taille des documents à 16 MB. Si la taille du documents est plus importante, il faut découper le document en plusieurs collections.


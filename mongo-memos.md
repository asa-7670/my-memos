# MONGODB

## C'est-quoi
    MongoDB est système de getsion de base de données orienté documents, répartissable sur un nembre quelconque d'ordinateur.
    MongoDB ne nécessite pas de schéma prédéfini des données.
    MongoDB est écrit en c++
    MongoDB fait partie de la mouvance NoSQL.
    L'objectif est de pouvoir gérer de grandes quantités de données.
    
## Site officiel    
    https://docs.mongodb.com/

## Tutorial en français
    https://buzut.fr/commandes-de-base-de-mongodb/
    
    https://openclassrooms.com/fr/courses/4462426-maitrisez-les-bases-de-donnees-nosql?status=published
    
    https://openclassrooms.com/fr/courses/4462426-maitrisez-les-bases-de-donnees-nosql/4474606-interrogez-vos-donnees-avec-mongodb     
    
## Installation
    Téléchargement : http://www.mongodb.org/downloads
    Suivre la documentation selon l'OS
    
    >sudo apt install mongoDB -> install mongoDB
    >mongod -> lance le serveur
    >mongo -> lance l'interpreteur de commandes

## Start service
    # Si la base de données n'est pas dans /data/db on doit spécifier le chemin avec --dbpath
    mongod --dbpath db/
    
    # si la base doit écouter sur un port spécifique
    mongod --port 42

    >mongod

## Stop service
    >sudo service mongodb stop
    
## Création de base de données
    # Mongodb ne fourni pas de commande pour créer une base de données.
    # Pas besoin de créér manuellement.
    # La base est créee lors de la première savegarde de la valeur dans la collection définie. 

## Importation de données
    $MONGO_HOME/bin/mongoimport --db new_data_base --collection new_collection $PATH_TO_FILE/import_file.json
    
    >MONGO/bin/mongoimport --db new_york --collection restaurants $RESTAURANT/restaurants.json

## Format des données
    # MongoDB enregistre les données dans le format BSON (format binaire de JSON)
    # Le format JSON (JavaScript Object Notation ) est utilisé pour l'insertion et la restitution des documents.
    
## Commandes

### Afficher la liste des bases de données
    show dbs
    
### Sélectionner une base de donnée
    use DATABASE_NAME
    
    > use cinemadb
    
### Afficher la liste des collections        
    show collections    
        
### Renomer une collection
    db.<COLLECTION_OLD_NAME>.renameCollection("<COLLECTION_NEW_NAME>")
    
    > db.actors.renameCollection("acteurs")
    
### Effacer une collection
    db.<COLLECTION_NAME>.drop()
    
    > use cinemadb
    > db.acteurs.drop()
    
### Effacer une base de données    
    use DATABASE_NAME
    db.dropDatabase()
    
    > use cinemadb
    > db.dropDatabase()            

### Ajouter un document->  insert | save
    use DATABASE_NAME
    db.<COLLECTION_NAME>.insert(<document>)
    
    >use cinemadb
    >db.actors.insert({"name": "Dupond", "lastname":"Martin"})
    
### Mise à jour d'un document -> update
     MongoDB mis à jour que le premier document trouvé.
     db.<COLLECTION_NAME>.update({<CRITERES>}, {<DOCUMENT>}})
     
     >use cinema
     >db.actors.update({"name":"Scarlette"},{"name":"Peter Pan", "age":"10"});
     

### Ajouter un nouveau champ au document -> $set   
    db.<COLLECTION_NAME>.update({<CRITERES>}, {$set:{<NOUVELLE_PROPRIETE: VALEUR}}, {multi:true | false})   
    
    >use cinemadb
    >db.actors.update({"name":"Scarlette"}, $set:{"age":"25}) -> ajoute la propriété age au premier document trouvé

### Renommer un champ dans un document -> $rename
    db.<COLLECTION_NAME>.update({<CRITERES>}, $rename:{"<OLD_NAME>", "<NEW_NAME"}, {multi:true | false})
    
    >use cinemadb
    >db.actors.update({'name':'Martin'}, $rename{'prenom', 'lastname'}, {multi:false})
    
### Supprimer un champ dans un document -> unset
    db.<COLLECTION8NAME>.update({CRITERE},$unset:{<PROPRIETE>:<VALEUR>}, {multi:true | false})
    
    >use cinemadb
    >db.<COLLECTION_NAME>.update({"name":"Scarlette"}, $unset:{"age":"25"})
    
### Insertion d'un tableau
    db.<COLLECTION_NAME>.insert({<CRITERE>, <ARRAY_NAME>:["<VALEURS>"]})
    
    >use cinemadb
    >db.actors.insert({"name":"Scarlette", tableau:['a','b','c']})
    
### Mise à jour d'un tableau
    db.<COLLECTION_NAME>.update({<CRITERE>},{$push:{<TABLE_NAME>:'value'}})
    
    >use cinemadb
    >db.actors.update({"name":"Scarlette"};{$push:{tab:'d'}}) 
    
    # $pushAll -> ajouter un tableau de valeur
    # $pop -> supprimer le dernier element du tableau
    # $addToSet, ajouter un element sans doublon

## Mise à jour multiple -> multi:true
    # {multi:true} -> modification plusieurs documents
    
    >db.actors.update({age:{$gt:25}},{multi:true})

### Séléction 

#### find
    # Tous les documents
    db.<COLLECTION_NAM>.find()
        
    # Avec Critères
    db.<COLLECTION_NAME>.find({<CRITERES>})

    >db.actors.find({"name":"Scarlette", "lastname":"Jonson"})
    
    # Dans un tableau contenant une valeur
    db.<COLLECTION_NAME>.find({<ARRAY_NAME>:'VALUE'})
    
    # Un élement parmi plusieurs
    db.<COLLECTION_NAME>.find({<ARRAY_NAME>:{$in:['value 1', 'value 2']}})
    
    # Combinaison de plusieurs
    db.<COLLECTION_NAME>.finf({<ARRAY_NAME>:{$all:['value 1', 'value 2']}})
    
    # OR 
    db.<COLLECTION_NAME>.find({$or:[{<CRITERE>}, {<CRITERE>}]})
    
    > db.actors.find({$or:[{'name':'Martin"},{'name':'Dupont'}]})
    
    # AND
    db.<COLLECTION_NAME>.find({$and:[{<CRITERE>},{<CRITERE>}]})
    
    > db.actors.find({$and:[{'name':'Martin'},{'lastname':'Dupont'},{'age':'25'}]})
    
    # Critères de recherche avec opérandes
    $gt : plus grand que
    $lt : plus petit que
    $gte : plus grand ou égal à
    $lte : plus petit ou égal à
    
    >db.produits.find({dixmill: {$gte:9997, $lt:9999 }})
    
    $or: pour récupérer les documents qui correspondent à 2 critères différents
    $and : pour cumuler des critères
    $in, $all, $exist, $type et $regex ...
 
#### distinct    
     db.<COLLECTION_NAME>.distinct("KEY_NAME")
     
     >db.actors.distinct("age")
     
#### projection
    Récupérer certaines propriétes
    db.<COLLECTION_NAME>.find({<CRITERES}, {<PROPRIETES_1>:1, <PROPRIETES_2>:1)
    
    >use cinemadb
    >db.actors.find({"name":"Scarlette"}, {lastname:1})
    
    lastename est retourné car listé avec la valeur 1.
    _id est systématiquement renvoyé.
    
    db.actors.find({},{_id:0, name:1}) -> _id  n'est pas renvoyé.

#### count
    db.<COLLECTION_NAME>.find({<CRITERES}).count()
    
    >use cinemadb
    >db.actors.find().count()
    
#### sort
    db.<COLLECTION_NAME>.find({<CRITERES}).sort({<PROPRIETE>:1})
    db.<COLLECTION_NAME>.find({<CRITERES}).sort({<PROPRIETE>:-1}) ->  -1 tri décroissant
    
    >use cinemadb
    >db.actors.find().sort(name:1)
    >db.actors.find().sort(name:-1) -> sens inverse
    
### group
    varGroup = { $group : {"_id" : "$KEY_GROUP_NAME", "Title" : {<function> : "$KEY_NAME"} } };
    db.<COLLECTION_NAME>.aggregate([varGroup])
    
    varUnwind = {$unwind : "$grades"}
    varGroup = { $group : {"_id" : "$borough", "moyenne" : {$avg : "$grades.score"} } };
    varSort = { $sort : { "moyenne" : -1 } }
    db.restaurants.aggregate([varUnwind, varGroup, varSort]);
    
### Supprimer un document -> remove
    # Tous les documents
    db.<COLLECTION_NAME>.remove({})
    
    # Documents sélectionnées
    db.<COLLECTION_NAME>.remove({<CRITERES})
 
## Remarques    
    # Une base de données mongo contient des collections dans lequelles des documents sont ajoutés.
    # Une collection est un ensemble de documents de me nature.
    # MongoDB limite la taille des documents à 16 MB. Si la taille du documents est plus importante, il faut découper le document en plusieurs collections.
    # MongoDB est schemaless, ce qui signifie que les documents ne doivent pas tous respecter le même format.
    # La console Mongo est aussi un shell JavaScript
    


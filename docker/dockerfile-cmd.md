## Crééer le fichier Dockerfile dans la racine deu projet et définir les instructions suivantes:

# FROM
    Permet de définir l'image source

# RUN
    Permet d’exécuter des commandes dans le conteneur

# ADD 
    Permet d'ajouter des fichiers dans le conteneur

# WORKDIR 
    Permet de définir votre répertoire de travail

# EXPOSE 
    Permet de définir les ports d'écoute par défaut

# VOLUME 
    Permet de définir les volumes utilisables (logs...)

# ENV
    Permet de définir de une variable d'environnement
    Exp: ENV NAME world

# CMD
    Permet de définir la commande par défaut lors de l’exécution de vos conteneurs Docker

# Exemple:
    FROM openclassrooms/build_image

    RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install nginx -y
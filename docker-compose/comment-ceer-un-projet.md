# 1- Creer un fichier docker-compose.yml à la racine du projet

# 2- Un fichier docker-compose commence toujour par ( version: 'NUM_VER_DOCKER_COMPOSE')

# 3- Décrire l'ensemble des ressources et services nécessaires à la réalisation du POC dans le fichier docker-compose.yml

# Exemple
# Projet wordpress 
## docker-compose.yml
    version: '3'
    services:
        db:
            image: mysql:5.7
            volumes:
                - db_data:/var/lib/mysql
            restart: always
            environement:
                MYSQL_ROOT_PASSWORD: somewordpress
                MYSQL_DATABASE: wordpress
                MYSQL_USER: wordpress
                MYSQL_PASSWORD: wordpress
        wordpress:
            depends_on:
                -db
            image: wordpress:latest
            ports:
                -"8000:80"
            restart: always
            environement:
                WORDPRESS_DB_HOST: db:3306
                WORDPRESS_DB_USER: wordpress
                WORDPRESS_DB_PASSWORD: wordpress
                WORDPRESS_DB_NAME: wordpress
    
    volumes:
        db_data:{}


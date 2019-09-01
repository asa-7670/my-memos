# Build image
    docker build -t NOM_IMAGE .
    -t: pour définir le nom de l'image à builder
    .: le répertoire ou setrouve le Dockerfile
    Exp: docker build -t MyFirstDockerImage

# Lancer docker
    docker run -d -p
    -d: pour détacher le conteneur du processus principal de la console
    -p: pour définir l'utilisation de ports. Transferer le trafic du port 8080 vers le port 80 du conteneur.
    Exp: docker run -d -p 8080:80 nginx

# Afficher l'ensemble des conteneurs existants
    docker ps

# Rentrer dans le docker
    docker exec -ti ID_RETOURNE_LORS_DU_DOCKER_RUN bash
    -ti: permet d'avoir un shell bash

# Arrêter un docker
    docker stop ID_RETOURNE_LORS_DU_DOCKER_RUN

# Supprimer un docker
    docker rm ID_RETOURNE_LORS_DU_DOCKER_RUN

# Récupérer une image du Docker Hub sans l'installée
    docker pull NOM_IMAGE (docker pull hello-world)

# Envoyer une image dans Docker hub
    docker tag local-image:tagname 
    username/new-repo:tagname
    Exp: docker tag oc-asa:latest toto/oc-asa:latest   

    docker push username/new-repo:tagname   
    Exp: docker push toto/oc-asa:latest 

# Chercher une image dans Docker hub
    docker search image
    Exp: docker search nginx

# Afficher l'ensemble des images présentes en local
    docker image ls -a

# Nettoyage du systeme:
    docker system prune
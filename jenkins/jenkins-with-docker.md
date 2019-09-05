# Installer Docker
    sudo apt-get install docker.io

# Ajouter les utilisdateurs:
    sudo addgroup docker
    sudo usermod -aG docker $UTILISATEUR
    Exp suod usermod -aG docker asa

# Installer l'image de Jenkins
    docker run \
    --name jenkins-master \
    -d -p 8080:8080 -p 50000:50000 \
    -v /var/jenkins_home \
    jenkins/jenkins:lts

    docker run : on lance une image
    --name jenkins-master : on lui donne un nom
    -d : en arrière plan
    -p x:y : le port y de la machine virtuelle est mappée sur le port x de l'hote
    -v chemin : on crée un volume pour garder les données de jenkins
    jenkins/jenkins:lts : nom de l'image à utiliser (prise depuis hub.docker.com)

# Débloquer Jenkins
    docker cp jenkins-master:/var/jenkins_home/secrets/initialAdminPassword .
    - installer le plugins
    - Créer le 1er utilsateur admin.

#Démarrer Jenkins
    docker start NOM_JENKINS_MAITRE
    Exp: docker start jenkins-master

# Arrêter Jenkins
    docker stop NOM_JENKINS_MAITRE
    Exp: docker stop jenkins-master
# Installer la machine maître de Jenkins en local:
    1 - Ajouter la clé du référentiel au système:
            wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    
    2 -  Ajouter l’adresse du référentiel de paquets Debian:
            sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    
    3- Mettre à jour le système:
        sudo apt-get update

    4 - Installer Jenkins
        sudo apt-get install jenkins

# Demarrer Jenkins comme un service
    sudo /etc/init.d/jenkins start
    sudo /etc/init.d/jenkins status
    OU
    sudo systemctrl start jenkins
    sudo systemctl status jenkins

# Débloquer Jenkins
    Le mot de passe admin est généré dans /var/lib/jenkins/secrets/initialAdminPassword

    sudo cat /var/lib/jenkins/secrets/initialAdminPassword

    - Installer le plugins.
    - Créer le 1er utilisateur Administrateur

# Arrêter Jenkins
    sudo /etc/init.d/jenkins stop
    OU
    sudo systemctl stop jenkins

# Désinstaller Jenkins
    sudo agt-get purge jenkins
    sudo agt-get update

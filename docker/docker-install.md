# Site officiel:
    https://hub.docker.com/
    https://docs.docker.com/get-started/


# Prés-requis:
    Pour installer Docker Engine - Community, vous avez besoin de la version 64 bits de l’une de ces versions d’Ubuntu:
    - Disco 19.04
    - Cosmic 18.10
    - Bionic 18.04 (LTS)
    - Xenial 16.04 (LTS)

# Désinstaller les anciennes versions
    sudo apt-get remove docker docker-engine docker.io containerd runc

# Mettre à jour votre système et installer les prérequis pour l'installation de Docker:
    sudo apt-get update && \
    sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

# Ajouter la clé officielle GPG de Docker:
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Ajouter le repository:
    sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"

# Installer Docker Engine - Community:
    sudo apt update && \
    sudo apt-get install \
    docker-ce \
    docker-ce-cli \
    containerd.io

# Verification de l'installtion du docker:
    sudo docker run hello-world

# Désinstaller Docker Engine-Community:
    sudo apt-get purge docker-ce
    sudo rm -rf /var/lib/docker
# C'est quoi?
    Docker compose un outil décrit en python qui permet de décrire dans un fichier YAML, plusieurs conteneurs comme un ensemble de services.
    
    Les conteneurs sont déclarés dans un fichier nomé docker-compose.yml

# Installtion
    sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose \
    && sudo chmod +x /usr/bin/docker-compose

# Vérification de l'installtion
    docker-compose --version

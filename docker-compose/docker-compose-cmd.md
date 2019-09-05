## Une stack est un ensemble de conteuneurs Docker lancés via un seul et unique ficier Docker compose.

# Démarrer une stack de Docker Compose
    docker-compose  up -d
    -d : en tache de fond

# Voir le statut d'une stack Docker Compose
    docker-compose ps

# Voir les logs d'une stack Docker Compose
    docker-compose logs -f --tail 5

# Arrêter une stack Docker Compose
    docker-compose stop

# Detruire l'ensemble des ressources d'une stack Docker Compose
    docker-compose down

# Valider une stack Docker Compose
    docker-compose config


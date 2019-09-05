# C'est quoi?
    Jenkins est un serveur web d'intégration construit suivant un modèle maître/esclave.
    
    Les projets sont configurées sur le serveur web sur la machine maître.
    
    les actions configuées sont sur les esclaves qui sont des instances lègères de Jinkins

    Chaque machine (maître ou eslave) posssède u ou plusieurs exécuteurs et chaque exécuteur peut faire une tâche à la fois.

# C'est quoi un module?
    Jenkins contient juste le nécessaire pour administrer le serveur (mettre en place les machine esclaves et éxecuter des commandes). Tout le reste des fonctionnalités ( récupération des sources à partir GIT, envoi d'emails lors d'un echec...) est implémentés sous forme de modules.

    Jenkins propose un gestionnaire de modules ( installer, supprimer ou mettre à jour un module)
    Le gestionnaire de module se trouve dans Jenkins -> Getion des modules.
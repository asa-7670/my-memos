## EDGE MICROSERVICES
	# Edge microservices Sont des Microservices spécialisés dans l'orchestration des Microservices centraux responsables de la logique de l'application.
	# Les Edge Microservices les plus populaires sont ceux publiés et utilisés par Netflix pour sa plateforme. Ils sont en grande partie regroupés sous Spring Cloud et disposent de fonctionnalités pour fonctionner nativement ensemble.

### Problème de configuration -> Spring Cloud Config
	Centralisé la configuration microservices avec Spring Cloud Config.

### Problème de découvabilité -> Eureka
	Grâce à une simple annotation, toute nouvelle instance de votre Microservice va être enregistrée auprès d'Eureka.

### Problème de Load Balancing -> Ribbon
	Ribbon (load Balancer) côté client est capable d'indiquer directement, depuis le Microservice, quelle instance du Microservice distant appeler.

### Problème de API Gateway -> Zuul
	# Zuul un point d'entrée unique vers les Microservices.
	# Plus besoin de sécuriser chaque Microservice, il suffit d'imposer les règles d'authentification et de sécurité à ZUUL.

### Problème de traçage des requêtes -> Zipkin
	# Zipkin permets de suivre les requêtes de Microservice en Microservice et de consulter les différentes réponses et interactions afin de cibler directement le problème. 
	

	

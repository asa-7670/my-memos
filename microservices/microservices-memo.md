## ARCHITECTURE MICROSERVICES

### Problématique
	1- Disponibilité des applications en ligne.(Scalabilité)
	2- Evolution fréquente des applications.
	3- Evolution rapide des technologies.

	Les entreprises doivent conçevoir leurs applications dès le départ à partir d'architectures répondant à ces besoins et qui sont parfaitement adaptées au cloud. C'est ainsi que l'architecture Microservices est apparue, apportant une réponse concrète à toutes ces préoccupations et la promesse d'obtenir, au bout, des applications dites "Cloud-native". 

### C'est quoi
	L'architecture Microservices propose une solution en principe simple : découper une application en petits services, appelés Microservices, parfaitement autonomes qui exposent une API REST que les autres Microservices pourront consommer.

### SOA VS MSA

### Spring Boot
	# Spring Boot est un framework qui permet de démarrer rapidement le développement d'applications ou services en fournissant les dépendances nécessaires et en auto-configurant celles-ci. Pour activer l'auto-configuration, on utilise l'annotation @EnableAutoConfiguration . Si vous écrivez vos propres configurations, celles-ci priment sur celles de Spring Boot.


### Les starters
	Les starters permettent d'importer un ensemble de dépendances selon la nature de l'application à développer afin de démarrer rapidement.
	Liste des starters disponible : https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-starter
	
	# spring-boot-starter-web : applications web.
	# spring-boot-starter-mail : plications et services d'envoi de mails.
	# spring-boot-starter-thymeleaf : application qui offre une interface utilisateur en utilisant le moteur de template thymeleaf.
	# spring-boot-starter-web-services : pour les services plus classiques utilisant SOAP.
	....

### Spring Initializr
	Outil qui permet la composition d'une application selon des besoins.
	http://start.spring.io -> Cliquez sur "Switch to the full version

### Annotation @SpringBootApplication	
	Une simple encapsulation de trois annotations :
	1- @Configuration : donne à la classe actuelle la possibilité de définir des configurations qui iront remplacer les traditionnels fichiers XML. Ces configurations se font via des Beans.
	2- @EnableAutoConfiguration : l'annotation vue précédemment qui permet, au démarrage de Spring, de générer automatiquement les configurations nécessaires en fonction des dépendances situées dans notre classpath.
	3- @ComponentScan : Indique qu'il faut scanner les classes de ce package afin de trouver des Beans de configuration.

### Fichier application.properties
	# Permet de modifier la configurations liées à Spring Boot et ses dépendances. Par exemple : changer le port d'écoute de Tomcat, l'emplacement des fichiers de log, les paramètres d'envoi d'emails
	# Liste des paramettres -> https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html

### Start microservice
	# Ligne de commande -> java -jar Path/vers/microservice/target/<microservice>.jar

### Annotation @RestController 
	# Indique que cette classe va pouvoir traiter les requêtes que nous allons définir. 
	# Indique aussi que chaque méthode va renvoyer directement la réponse JSON à l'utilisateur, donc pas de vue dans le circuit.

### Annotation @Repository 
	Cette annotation est appliquée à la classe afin d'indiquer à Spring qu'il s'agit d'une classe qui gère les données, ce qui nous permettra de profiter de certaines fonctionnalités comme les translations des erreurs.

### Filtrage static 

#### Annotation @JsonIgnore
	Au-dessus des propriétés pour la cachée.
	
	@JsonIgnore
    	private int prixAchat;

#### Annotation @JsonIgnoreProperties
	Pour ignorer plusieurs propriétes à la fois

	@JsonIgnoreProperties(value = {"prixAchat", "id"})
	public class Product {
	  ...
	}

### Filtrage dynamique

#### Annotation @JsonFilter("monFiltreDynamique")

	@JsonFilter("monFiltreDynamique")
	public class Product {
	...
	}

### Base de données
	- @Entite
	- @Id
	- @GenaratedValue

##### JPA
	# Liste des méthodes JPA : https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html
	# Mots clé acceptés : https://docs.spring.io/spring-data/data-jpa/docs/1.1.x/reference/html/#jpa.query-methods.query-creation

#### Base de données H2 
	# Très simple à mettre en place et complètement auto-configurée par Spring Boot.
	# Créer les tables et les données uniquement en mémoire vive.
	 <dependency>
	    <groupId>com.h2database</groupId>
	    <artifactId>h2</artifactId>
	    <scope>runtime</scope>
	 </dependency>
	
	# Configurations H2
	spring.jpa.show-sql=true
	spring.h2.console.enabled=true
	
	# Console H2 disponible au -> http://<host>:<port>/h2-console/
	# JDBC URL ->  jdbc:h2:mem:testdb
	# user SA



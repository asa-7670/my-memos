## PROGRAMATION ORIENTE OBJET

### SOLID
	SOLID est un acronyme permettant de se rappeler 5 principes de conception en programmation orientée objet afin d'obtenir une application plus fiable et plus robuste :
	1- Single responsibility principle (responsabilité unique)
	2- Open/closed principle (ouvert/fermé)
	3- Liskov substitution principle (substitution de Liskov)
	4- Interface segregation principle (ségrégation des interfaces)
	5- Dependency inversion principle (inversion des dépendances)

### Injection de dépendances
	1- Au déploiement de l'application, la class DependencyInjectionListener est instanciée par le serveur d'application.
	2- Le serveur appel ensuite la méthode contextInitialized(ServletContextEvent) sur l'instance qu'il vient de créer.
	3- Cette méthode crée l'instance de MAnagerFactory et l'inject dans l'attribut static dédié (managerFactory) de la classe AbstractResource. 

### Bonnes pratiques
	Pour mieux respecter le principe de dependency inversion et les avantages qu'il procure, il faudrait dissocier les interfaces des implémentations, en les mettant dans des packages différents et des modules Maven séparés.

	Exemple :

	module ticket-business

	package de base org.example.ticket.business.contract

	module ticket-business-impl

	package de base org.example.ticket.business.impl

	Cela dit, pour de petits projets, où les modules ne sont pas partagés entre plusieurs applications, il est acceptable de simplement séparer les interfaces et les implémentations dans des packages différents, tout en les laissant dans le même module Maven.

### Resumé
	Petit résumé de ce que nous avons vu, avant de passer à la suite :

	Les classes doivent avoir une seule raison de changer : ne gérez pas le cycle de vie des classes des couches inférieures dans les classes des couches supérieures. Faites de l'inversion de contrôle (IoC) grâce à des Factories et de l'injection de dépendances (DI).

	Les classes des couches supérieures ne dépendent pas des classes d'implémentations des couches inférieures, mais d'abstractions.

	Les classes des couches inférieures implémentent ces abstractions. Elles en dépendent donc.

	Les abstractions ne doivent pas dépendre des détails : n'orientez pas les abstractions en fonction de l'implémentation prévue.

	Les abstractions sont réalisées avec des interfaces.

	Celles-ci permettent d'écrire le contrat d'échange entre les couches supérieures et l'implémentation faites dans les couches inférieures.

### Injection
	@Inject (JSR-330)
	@Autowired (spring)
	@ManagedBean (JSR-250)
	@Named (JSR-330) 
	@Component (Spring)
	

## Spring Cloud Config

	#application.properties  peut être utilisé pour stocker des constantes auxquelles on peut accéder grâce à un bean annoté avec  @ConfigurationProperties.
	#Config-Server permet de récupérer les fichiers de configuration dans un dépôt et de les servir aux Microservices en se basant sur leurs noms.
	#Pour récupérer automatiquement ces configurations, il suffit d’ajouter le starter spring-cloud-starter-config et de renommer application.properties en bootstrap.properties.
	#Pour actualiser à la volée la configuration d’un Microservice en l’obligeant à récupérer une version fraîche du fichier .properties, il suffit d’envoyer un POST vers l'endpoint /refresh exposé par Spring Actuator

### Configuration

#### Microservice Serveur

##### POM
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-config</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-config-server</artifactId>
	</dependency>

##### Classe Config
	@SpringBootApplication
	@EnableConfigServer
	public class ConfigServerApplication {
		public static void main(String[] args) {
			SpringApplication.run(ConfigServerApplication.class, args);
		}

	}

##### Bootstrap
	#boostrap.yml
	spring:
		application:
			name: configServer
		profiles:
			active: native
		cloud:
			config:
				server:
					native:
						search-locations:  classpath:/config/,
							classpath:/config/commandes.properties
	server:
		servlet:
			context-path: /asaConfigServer
		port: 9999


	# url: http://localhost:9100/commandes/default.

#### Microservice client

##### POM
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-config</artifactId>
	</dependency>

##### Bootstrap
	#bootstrap.yml
	spring:
  		application:
    			name: client-ui
  	profiles:
    		active: native
  	cloud:
    		config:
      			uri:  http://localhost:9999/ConfigServer
      			fail-fast : true



## Spring Eureka
    # Eureka est un annuaire de services.

### Configuration

#### Microservice serveur
##### Pom
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-config</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
	</dependency>

	<dependency>
		<groupId>com.google.code.gson</groupId>
		<artifactId>gson</artifactId>
		<version>${gson.version}</version>
	</dependency>

##### Bootstrap
	spring.application.name=eureka-server
	server.port=8761
	eureka.client.registerWithEureka:false
	eureka.client.fetchRegistry:false

##### Classe
	@SpringBootApplication
	@EnableEurekaServer
	public class EurekaServerApplication {
		public static void main(String[] args) {
			SpringApplication.run(EurekaServerApplication.class, args);
		}

	}
##### URL
	# Admin: http://localhost:8761/
	# Service : http://localhost:8761/eureka/

#### Mcroservice client
##### Pom
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
	</dependency>

##### Classe
	@SpringBootApplication
	@EnableDiscoveryClient
	public class ProduitsApplication {
		public static void main(String[] args) {
			SpringApplication.run(ProduitsApplication.class, args);
		}

	}

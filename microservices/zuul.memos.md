## Spring ZUUL
	# ZUUL se positionner comme le point d'entrée unique d'une application. 
	# ZUUL s'occupe de dispatcher, modifier et appliquer des filtres et des règles à ces requêtes.

### Configuration

#### POM
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
	</dependency>

#### Classe
	@SpringBootApplication
	@EnableZuulProxy
	@EnableDiscoveryClient
	public class ZuulServerApplication {
		public static void main(String[] args) {
			SpringApplication.run(ZuulServerApplication.class, args);
		}
	}

#### micro-service

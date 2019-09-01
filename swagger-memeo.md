## SWAGGER

### C'est quoi
	# Fromwork qui permet de générer une documentation détaillée au format JSON,
	# Répondant aux spécificationsOpenAPI. 
	# Offre également la possibilité de visualiser cette documentation dans un format HTML élégant.


### Site officiel
	# https://swagger.io/specification/

### Documentation 
	# https://springfox.github.io/springfox/docs/current/#docket-spring-java-configuration

### Maven
	
	<dependency>
		<groupId>io.springfox</groupId>
		<artifactId>springfox-swagger2</artifactId>
		<version>2.8.0</version>
	</dependency>
	<dependency>
		<groupId>io.springfox</groupId>
		<artifactId>springfox-swagger-ui</artifactId>
		<version>2.8.0</version>
	</dependency>

### Exemple Minimum

	package com.ecommerce.microcommerce;

	import org.springframework.boot.SpringApplication;
	import org.springframework.boot.autoconfigure.SpringBootApplication;
	import springfox.documentation.swagger2.annotations.EnableSwagger2;

	@SpringBootApplication
	@EnableSwagger2
	public class MicrocommerceApplication {

		public static void main(String[] args) {
			SpringApplication.run(MicrocommerceApplication.class, args);
		}
	}

### Exemple personalisé
	1- Classe de configuration any
		package com.ecommerce.microcommerce.configuration;
		import org.springframework.context.annotation.Bean;
		import org.springframework.context.annotation.Configuration;
		import springfox.documentation.builders.PathSelectors;
		import springfox.documentation.builders.RequestHandlerSelectors;
		import springfox.documentation.spi.DocumentationType;
		import springfox.documentation.spring.web.plugins.Docket;
		import springfox.documentation.swagger2.annotations.EnableSwagger2;

		@Configuration
		@EnableSwagger2
		public class SwaggerConfig {
		@Bean
		public Docket api() {
			return new Docket(DocumentationType.SWAGGER_2)
				.select()
				.apis(RequestHandlerSelectors.any())
				.paths(PathSelectors.any())
				.build();
			}
		}	

	2- Classe de configuration filtrée
		package com.ecommerce.microcommerce.configuration;

		import org.springframework.context.annotation.Bean;
		import org.springframework.context.annotation.Configuration;
		import springfox.documentation.builders.PathSelectors;
		import springfox.documentation.builders.RequestHandlerSelectors;
		import springfox.documentation.spi.DocumentationType;
		import springfox.documentation.spring.web.plugins.Docket;
		import springfox.documentation.swagger2.annotations.EnableSwagger2;

		@Configuration
		@EnableSwagger2
		public class SwaggerConfig {

		@Bean
		public Docket api(){
			return new Docket(DocumentationType.SWAGGER_2)
				.select()
				.apis(RequestHandlerSelectors.basePackage("com.ecommerce.microcommerce.web"))
				.paths(PathSelectors.regex("/Produits.*"))
				.build();
			}
		}
	
	3- dans le controller
		@Api( description="API pour es opérations CRUD sur les produits.")
		@RestController
		public class ProductController {
		    .....
		}

	4- pour chaque méthode
		//Récupérer un produit par son Id
		@ApiOperation(value = "Récupère un produit grâce à son ID à condition que celui-ci soit en stock!")
		@GetMapping(value = "/Produits/{id}")
		public Product afficherUnProduit(@PathVariable int id) {
		......
		}

### Format de sortie
	# Json -> http://localhost:9090/v2/api-docs. 
	# html -> http://localhost:9090/swagger-ui.html
		

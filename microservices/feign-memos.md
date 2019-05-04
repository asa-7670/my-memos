## Spring Feign

	# Feign est un outil qui permet la simplification de la communication entre Microservices, en générant automatiquement les requêtes HTTP à partir des données fournies dans des classes appelées proxies.
	# Une fois la réponse du Microservice distant reçue, Feign l'associe à un bean local que l'on aura créé. On obtient alors en retour directement des objets java prêts à l'emploi.
	# Quand Feign rencontre un autre code de réponse que 2XX, il génère une exception  FeignException . Afin de pouvoir décoder la réponse et extraire les bons codes d'erreur, il faut créer une classe qui hérite de  ErrorDecoder et qui implémente  decode

### Configuration
#### POM
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-openfeign</artifactId>
	</dependency>

#### Classe
	@SpringBootApplication
	@EnableDiscoveryClient
	@EnableFeignClients("com.asa.app.microservices.client.proxy")
	public class ClientUiApplication {
		public static void main(String[] args) {
			SpringApplication.run(ClientUiApplication.class, args);
		}
	}


#### Proxy
	@FeignClient(name = "asa-microservice-produits", url = "localhost:9010")
	public interface ProductProxy {
	    @GetMapping(value = "/Produits")
	    List<Product> listeDesProduits();

	    @GetMapping( value = "/Produits/{uuid}")
	    Product recupererUnProduit(@PathVariable UUID uuid);
	}

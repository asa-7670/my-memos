## Spring Ribbon
	# Ribbon est un équilibreur de charge côté client. Une fois installé, il va pouvoir aller consulter la liste des instances disponibles pour un Microservice pour les choisir à tour de rôle afin d'équilibrer la charge.

	# Pour tester Ribbon, nous devons tout d'abord lancer plusieurs instances du Microservice-produits qui feront l'objet de nos tests.

	# Pour lancer différentes instances d'un Microservice, vous pouvez soit utiliser Docker, soit les lancer sur différents ports. (-Dserver.port=9001)

### Configuration

#### POM
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
	</dependency>
	<dependency>
		<groupId>org.apache.httpcomponents</groupId>
		<artifactId>httpclient</artifactId>
	</dependency>

#### Classe proxy 
	@FeignClient(name = "microservice-produits")
	@RibbonClient(name = "microservice-produits")

	public interface MicroserviceProduitsProxy {
	  
	  @GetMapping(value = "/Produits")
	  List<ProductImpl> getProducts();

	  /*
	  * Notez ici la notation @PathVariable("uuid") qui est différente de celle qu'on utlise dans le contrôleur
	  **/
	  @GetMapping( value = "/Produits/{uuid}")
	  ProductImpl getProduct(@PathVariable("uuid") int uuid);
	}


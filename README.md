# Microservice
Pour développer ses microservices simples nous allons utiliser Spring Cloud, Spring Boot et Eureka Server.

Eureka Server nous servira de registre de services.

Nous avons développer deux microservices:
  - hello-service qui ne fera que renvoyer "hello"
  - hello-web-client-service traitera la demande provenant d'un client. Il appellera "hello-service" et retournera une page Web en réponse
  
Il y aura trois serveurs distincts:
  - Eureka
  - hello-service
  - hello-web-client-service
  
Donc en définitive il y aura 3 projets maven.

# Eureka server
    Maven Dependencies
  
     <dependency>
     <groupId>org.springframework.cloud</groupId>
     <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
     </dependency>

    Configuration
    
      Application.properties
    
    - server.port=8761
    - eureka.client.register-with-eureka=false
    - eureka.client.fetch-registry=false
    
Il est indispensable d'ajouter "@EnbleEurekaServer" dans la main class d'éxécution d'Ereka server.
Il ne rest eplus qu'à accéder au server Eureka sur http://localhost:8761

# Hello-service
    
     <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
     </dependency>

     <dependency>
     <groupId>org.springframework.cloud</groupId>
     <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
     </dependency>

Création de l'entity HelloObject
création de HelloController

    Configuration
    
      application.properties
      
    - eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka/
    - #running for multiple instances
    - server.port=${PORT:0}
    - eureka.instance.instance-id=${spring.application.name}:${spring.application.instance_id:${random.value}}
    
      bootstrap.properties
      
    - spring.application.name=hello-service

Le fichier bootstrap.properties correspond au contexte de bootstrap (le contexte parent de l'application principale) utilisant une convention de localisation de
configuration externe différente de celle du contexte de l'application principale.

Il faut faire figurer l'annotation "@EnableDiscoveryClient"
Après exécution de l'instance "hello-service" nous avons l'application HELLO-SERVICE qui apparait sur spring Eureka.

# Hello-Web-Client-Service

    Maven Dependencies
    
    	<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-thymeleaf</artifactId>
	</dependency>
    
En plus des autres dependencies vue au dessus nous aurons besoin de la dependencies pour intégrer le thymeleaf.
    

 


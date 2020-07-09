# Microservice
Pour développer ses microservices simples nous allons utiliser Spring Cloud, Spring Boot et Eureka Server.

Eureka Server nous servira de registre de services.

Nous avons développer deux microservices:
  - hello-service qui ne fera que renvoyer "hello"
  - hello-web-client-service traitera la demande provenant d'un client. Il appellera "hello-service" et retournera une page Wev en réponse
  
Il y aura trois serveurs distincts:
  - Eureka
  - hello-service
  - hello-web-client-service
  
Donc en définitive il y aura 3 projets maven.

# Eureka server
  # Maven Dependencies
  
  - <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
    </dependency>

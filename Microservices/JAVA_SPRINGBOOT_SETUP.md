# 🚀 Java Spring Boot Microservice Setup Guide

## Overview

This guide walks you through setting up a basic Java Spring Boot microservice with essential components like REST APIs, service discovery (Eureka), and centralized configuration.

---

## 1. Create Spring Boot Project
    - Go to [Spring Initializr](https://start.spring.io/)
    - Select:
      - Project: Maven or Gradle
      - Language: Java
      - Spring Boot version (e.g., 3.x.x)
      - Dependencies:
        - Spring Web
        - Spring Boot Actuator
        - Spring Data JPA (if DB needed)
        - Eureka Discovery Client (`spring-cloud-starter-netflix-eureka-client`)
        - Spring Cloud Config Client (`spring-cloud-starter-config`)
    
    Download and extract the project.

---

## 2. Configure `application.yml`
    ```yaml
    server:
      port: 8081
    
    spring:
      application:
        name: my-microservice
      datasource:
        url: jdbc:mysql://localhost:3306/mydb
        username: user
        password: pass
    
    eureka:
      client:
        service-url:
          defaultZone: http://localhost:8761/eureka/
          
## 3. Enable Eureka Client
    In your main application class:
    @SpringBootApplication
    @EnableEurekaClient
    public class MyMicroserviceApplication {
      public static void main(String[] args) {
        SpringApplication.run(MyMicroserviceApplication.class, args);
      }
    }

## 4. Create a Simple REST Controller
    @RestController
    @RequestMapping("/api")
    public class HelloController {
    
      @GetMapping("/hello")
      public String sayHello() {
        return "Hello from Spring Boot Microservice!";
      }
    }

## 5. Run Eureka Server (Service Registry)    
    Create a new Spring Boot app with dependency spring-cloud-starter-netflix-eureka-server.
    @SpringBootApplication
    @EnableEurekaServer
    public class EurekaServerApplication {
      public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
      }
    }
    application.yml:
    
    yaml
    Copy
    Edit
    server:
      port: 8761
    
    eureka:
      client:
        register-with-eureka: false
        fetch-registry: false
    Start Eureka Server before running your microservice.

## 6. Centralized Configuration (Optional)
    Set up a Spring Cloud Config Server:
    Dependency: spring-cloud-config-server
    Annotate main class with @EnableConfigServer
    Point to your config repository (Git or filesystem)
    Microservices fetch config on startup.

## 7. Build and Run
    Use Maven or Gradle to build:
    ./mvnw clean package

## Run microservice:
    java -jar target/my-microservice.jar

## 8. Test the Microservice
    Access endpoint in browser or Postman:
    http://localhost:8081/api/hello
    You should see:
    Hello from Spring Boot Microservice!

## Next Steps
    Add database support (Spring Data JPA)
    Secure APIs with Spring Security & OAuth2
    Implement resilience patterns (circuit breaker, fallback)
    Add API Gateway (Spring Cloud Gateway)
    Containerize with Docker
    Deploy to Kubernetes or cloud platform

    








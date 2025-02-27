# Spring Boot and Microservices Interview Questions

## Table of Contents

### 1. **Spring Boot & Spring Concepts**
- [1.1 Concept of Spring and Spring Boot](#concept-of-spring-and-spring-boot)
- [1.2 Spring Boot vs Spring MVC](#spring-boot-vs-spring-mvc)
- [1.3 How to Create a Spring Boot Application](#how-to-create-a-spring-boot-application)
- [1.4 Spring Boot vs Spring](#spring-boot-vs-spring)
- [1.5 Features of Spring Boot](#features-of-spring-boot)

### 2. **Dependency Injection & Inversion of Control (IoC)**
- [2.1 Dependency Injection in Spring](#dependency-injection-in-spring)
- [2.2 Types of Dependency Injection](#types-of-dependency-injection)
- [2.3 Inversion of Control (IoC) Container](#inversion-of-control-ioc-container)
- [2.4 Advantages of Dependency Injection](#advantages-of-dependency-injection)
- [2.5 How Dependency Injection Works in Security](#how-dependency-injection-works-in-security)

### 3. **Spring Boot Beans & Scopes**
- [3.1 Bean Scopes in Spring Boot](#bean-scopes-in-spring-boot)
- [3.2 Singleton vs Prototype Scopes](#singleton-vs-prototype-scopes)
- [3.3 Ways to Create Beans in Spring Boot](#ways-to-create-beans-in-spring-boot)
- [3.4 Autoconfiguration of External Jars in Spring Boot](#autoconfiguration-of-external-jars-in-spring-boot)
- [3.5 Primary & Qualifier Annotations for Bean Injection](#primary-qualifier-annotations-for-bean-injection)
- [3.6 Spring Bean Lifecycle](#spring-bean-lifecycle)

### 4. **Microservices Architecture**
- [4.1 Microservices vs Web Services](#microservices-vs-web-services)
- [4.2 Microservices Communication](#microservices-communication)
- [4.3 Service Discovery, API Gateway, and Load Balancing](#service-discovery-api-gateway-and-load-balancing)
- [4.4 How Microservices Handle Fault Tolerance](#how-microservices-handle-fault-tolerance)
- [4.5 Circuit Breaker & Rate Limiter in Microservices](#circuit-breaker-rate-limiter-in-microservices)
- [4.6 Identifying Service Failures in Microservices](#identifying-service-failures-in-microservices)
- [4.7 Microservices Monitoring and Logging](#microservices-monitoring-and-logging)
- [4.8 Spring AOP in Microservices](#spring-aop-in-microservices)
- [4.9 How to Ensure 90% Availability in Production for Microservices](#how-to-ensure-90-availability-in-production-for-microservices)

### 5. **Spring Boot Annotations**
- [5.1 Stereotype Annotations in Spring](#stereotype-annotations-in-spring)
- [5.2 Custom Annotations in Spring Boot](#custom-annotations-in-spring-boot)
- [5.3 @Async and @Future Annotations](#async-and-future-annotations)
- [5.4 @Transactional Annotation](#transactional-annotation)

### 6. **REST API Design & Implementation**
- [6.1 Rest API Design and Flow](#rest-api-design-and-flow)
- [6.2 How REST API Works Internally](#how-rest-api-works-internally)
- [6.3 Methods in REST API: Idempotency](#methods-in-rest-api-idempotency)
- [6.4 REST API with CRUD Operations](#rest-api-with-crud-operations)
- [6.5 Path Parameters vs Query Parameters](#path-parameters-vs-query-parameters)
- [6.6 Error Handling in REST API](#error-handling-in-rest-api)
- [6.7 Different HTTP Methods in REST API (GET, POST, PUT, DELETE)](#different-http-methods-in-rest-api-get-post-put-delete)

### 7. **JPA and Database Integration**
- [7.1 Connecting to Database in Spring Boot](#connecting-to-database-in-spring-boot)
- [7.2 Working with JPA in Spring Boot](#working-with-jpa-in-spring-boot)
- [7.3 Using MongoDB with Spring Boot](#using-mongodb-with-spring-boot)
- [7.4 Configuring Multiple Database Connections](#configuring-multiple-database-connections)
- [7.5 Database Transactions and Rollback](#database-transactions-and-rollback)

### 8. **Security in Microservices**
- [8.1 Authentication Methods in Microservices](#authentication-methods-in-microservices)
- [8.2 JWT Token Usage in Microservices](#jwt-token-usage-in-microservices)
- [8.3 Handling Security in Microservices](#handling-security-in-microservices)

### 9. **Monitoring and Debugging**
- [9.1 Monitoring Spring Boot Applications](#monitoring-spring-boot-applications)
- [9.2 Debugging Issues in Microservices](#debugging-issues-in-microservices)
- [9.3 Tracing in Microservices](#tracing-in-microservices)

### 10. **Caching in Spring Boot**
- [10.1 Implementing Caching in Spring Boot](#implementing-caching-in-spring-boot)
- [10.2 Caching in Microservices](#caching-in-microservices)

### 11. **Testing and Deployment**
- [11.1 Testing in Spring Boot and Microservices](#testing-in-spring-boot-and-microservices)
- [11.2 How to Handle Unexpected Traffic Spikes](#how-to-handle-unexpected-traffic-spikes)
- [11.3 Deployment and Availability of Microservices](#deployment-and-availability-of-microservices)

### 12. **Additional Topics**
- [12.1 Swagger API Integration in Spring Boot](#swagger-api-integration-in-spring-boot)
- [12.2 Resource Server in Spring Boot](#resource-server-in-spring-boot)
- [12.3 Rate Limiting Implementation in Microservices](#rate-limiting-implementation-in-microservices)
- [12.4 Orchestration vs Choreography in Microservices](#orchestration-vs-choreography-in-microservices)
- [12.5 Difference between PUT and PATCH HTTP Methods](#difference-between-put-and-patch-http-methods)
- [12.6 Spring Actuator for Health and Performance Monitoring](#spring-actuator-for-health-and-performance-monitoring)

---

## 1. **Spring Boot & Spring Concepts**

### 1.1 Concept of Spring and Spring Boot
- **Spring**: A framework that provides comprehensive infrastructure support for developing Java applications. It focuses on Dependency Injection, Aspect-Oriented Programming, and simplifies Java development with a set of reusable components.
- **Spring Boot**: A streamlined version of the Spring framework designed to simplify the setup and configuration of Spring applications. It includes embedded servers and eliminates the need for complex configuration files.

### 1.2 Spring Boot vs Spring MVC
- **Spring MVC**: A web framework used for developing web applications in the Spring ecosystem. It is part of the broader Spring framework.
- **Spring Boot**: A tool that makes it easier to create stand-alone, production-grade Spring-based applications, which includes Spring MVC as one of its components.

### 1.3 How to Create a Spring Boot Application
- Use Spring Initializr to generate the project setup or manually configure your `application.properties` and `pom.xml` (or `build.gradle`) files.

### 1.4 Spring Boot vs Spring
- **Spring Boot** simplifies the setup of Spring applications, automatically configuring components and providing an embedded server.
- **Spring** requires more manual configuration and setup of components.

### 1.5 Features of Spring Boot
- Auto-configuration, embedded servers, minimal configuration, Spring Boot Starters, and Spring Boot Actuator.

---

## 2. **Dependency Injection & Inversion of Control (IoC)**

### 2.1 Dependency Injection in Spring
- A design pattern used to implement IoC, where the Spring container injects the dependencies into a class rather than the class creating them.

### 2.2 Types of Dependency Injection
- Constructor Injection, Setter Injection, and Field Injection.

### 2.3 Inversion of Control (IoC) Container
- A container that manages object creation and the lifecycle of beans.

### 2.4 Advantages of Dependency Injection
- Loose coupling, easier testing, and better maintainability.

### 2.5 How Dependency Injection Works in Security
- Spring Security uses DI to inject necessary security components, such as authentication and authorization mechanisms, into your application.

---

## 3. **Spring Boot Beans & Scopes**

### 3.1 Bean Scopes in Spring Boot
- Singleton, Prototype, Request, Session, and Global Session scopes.

### 3.2 Singleton vs Prototype Scopes
- **Singleton**: One instance is shared across the application.
- **Prototype**: A new instance is created each time a bean is requested.

### 3.3 Ways to Create Beans in Spring Boot
- Through annotations such as `@Component`, `@Service`, `@Repository`, or `@Bean` method in configuration classes.

### 3.4 Autoconfiguration of External Jars in Spring Boot
- Spring Boot can automatically configure dependencies in your project via its `spring-boot-starter` dependencies.

### 3.5 Primary & Qualifier Annotations for Bean Injection
- `@Primary` helps Spring decide which bean to inject when there are multiple candidates.
- `@Qualifier` specifies which bean to inject when multiple beans of the same type are available.

### 3.6 Spring Bean Lifecycle
- The lifecycle includes instantiation, dependency injection, initialization, and destruction.

---

## 4. **Microservices Architecture**

### 4.1 Microservices vs Web Services
- **Microservices**: A software architecture style where applications are developed as a set of loosely coupled services, each responsible for a specific task.
- **Web Services**: A service offering over the web, which can be SOAP-based or RESTful.

### 4.2 Microservices Communication
- Microservices communicate using protocols like HTTP (REST), gRPC, or messaging systems (Kafka, RabbitMQ).

### 4.3 Service Discovery, API Gateway, and Load Balancing
- **Service Discovery**: Tools like Eureka or Consul help microservices discover each other.
- **API Gateway**: A single entry point for all client requests, which handles routing and load balancing.
- **Load Balancing**: Distributes client requests across instances of a service to ensure high availability.

---

## 5. **Spring Boot Annotations**

### 5.1 Stereotype Annotations in Spring
- `@Component`, `@Service`, `@Repository`, and `@Controller` are used to mark classes as Spring beans for automatic detection.

### 5.2 Custom Annotations in Spring Boot
- Custom annotations can be created using `@interface` to define your own set of behaviors.

---

## 6. **REST API Design & Implementation**

### 6.1 Rest API Design and Flow
- REST APIs use HTTP methods (GET, POST, PUT, DELETE) to interact with resources, which are represented by URLs.

### 6.2 How REST API Works Internally
- Client sends a request, the server processes it, and the response is sent back. It follows the principles of stateless communication and resource-based addressing.

---

## 7. **JPA and Database Integration**

### 7.1 Connecting to Database in Spring Boot
- Use `application.properties` or `application.yml` to configure database connection settings.

### 7.2 Working with JPA in Spring Boot
- Create entity classes annotated with `@Entity` and repositories extending `JpaRepository`.

---

## 8. **Security in Microservices**

### 8.1 Authentication Methods in Microservices
- Common methods include OAuth2, JWT, and Basic Authentication for securing microservices.

---

## 9. **Monitoring and Debugging**

### 9.1 Monitoring Spring Boot Applications
- Use Spring Boot Actuator and external tools like Prometheus and Grafana for monitoring.

---

## 10. **Caching in Spring Boot**

### 10.1 Implementing Caching in Spring Boot
- Enable caching with `@EnableCaching` and use annotations like `@Cacheable` to cache method results.

---

## 11. **Testing and Deployment**

### 11.1 Testing in Spring Boot and Microservices
- Use tools like JUnit, Mockito, and Spring Test for unit and integration testing.

---

## 12. **Additional Topics**

### 12.1 Swagger API Integration in Spring Boot
- Swagger is a tool for documenting REST APIs, typically integrated using `springfox-swagger2` and `springfox-swagger-ui` libraries.

---


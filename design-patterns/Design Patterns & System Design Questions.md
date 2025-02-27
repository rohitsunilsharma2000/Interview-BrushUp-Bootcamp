# Design Patterns & System Design Index

Welcome to the index page for Design Patterns and System Design solutions. This page provides a navigation guide to various design patterns, system design concepts, and practical implementations.

---

## Table of Contents

### 1. [Design Patterns](#1-design-patterns)
   - [1.1 Singleton Pattern](#11-singleton-pattern)
   - [1.2 Chain of Responsibility Pattern](#12-chain-of-responsibility-pattern)
   - [1.3 Decorator Design Pattern](#13-decorator-design-pattern)
   - [1.4 Factory Design Pattern](#14-factory-design-pattern)
   - [1.5 Prototype Design Pattern](#15-prototype-design-pattern)
   - [1.6 Abstract Factory Design Pattern](#16-abstract-factory-design-pattern)
   - [1.7 Builder Design Pattern](#17-builder-design-pattern)
   - [1.8 Adapter Design Pattern](#18-adapter-design-pattern)
   - [1.9 Circuit Breaker Design Pattern](#19-circuit-breaker-design-pattern)
   - [1.10 Saga Design Pattern](#110-saga-design-pattern)

### 2. [System Design](#2-system-design)
   - [2.1 Queue and Stack Data Structures](#21-queue-and-stack-data-structures)
   - [2.2 Producer and Consumer Problem](#22-producer-and-consumer-problem)
   - [2.3 Load Balancer](#23-load-balancer)
   - [2.4 Auto Scaling](#24-auto-scaling)
   - [2.5 Distributed Tracing](#25-distributed-tracing)
   - [2.6 Monitoring Application Health](#26-monitoring-application-health)
   - [2.7 Microservices Architecture](#27-microservices-architecture)
   - [2.8 Subscription Service Design](#28-subscription-service-design)

### 3. [System Design Projects](#3-system-design-projects)
   - [3.1 TinyURL (URL Shortener) System Design](#31-tinyurl-url-shortener-system-design)
   - [3.2 Retail Product Advertisement Add-on Service](#32-retail-product-advertisement-add-on-service)

### 4. [Performance Optimization](#4-performance-optimization)
   - [4.1 Handling Large Requests in Payment Services](#41-handling-large-requests-in-payment-services)

### 5. [Design Patterns in Projects](#5-design-patterns-in-projects)

### 6. [Miscellaneous Topics](#6-miscellaneous-topics)
   - [6.1 Strangler Design Pattern](#61-strangler-design-pattern)
   - [6.2 API Design Patterns](#62-api-design-patterns)
   - [6.3 Sharding vs Partitioning](#63-sharding-vs-partitioning)
   - [6.4 Singleton and Static Design Patterns](#64-singleton-and-static-design-patterns)

---

## 1. Design Patterns

### 1.1 Singleton Pattern
- [Explanation of the Singleton pattern](#explanation-of-the-singleton-pattern)
- [Thread-safety in Singleton pattern](#thread-safety-in-singleton-pattern)
- [Code Implementation of Singleton pattern](#code-implementation-of-singleton-pattern)

### 1.2 Chain of Responsibility Pattern
- [Use of the Chain of Responsibility pattern](#use-of-the-chain-of-responsibility-pattern)

### 1.3 Decorator Design Pattern
- [Explanation of Decorator Design Pattern](#explanation-of-decorator-design-pattern)
- [How it works](#how-it-works)

### 1.4 Factory Design Pattern
- [Explanation of the Factory Design Pattern](#explanation-of-the-factory-design-pattern)
- [Implementation of Factory Design Pattern](#implementation-of-factory-design-pattern)

### 1.5 Prototype Design Pattern
- [Explanation of Prototype Design Pattern](#explanation-of-prototype-design-pattern)

### 1.6 Abstract Factory Design Pattern
- [Explanation of Abstract Factory Design Pattern](#explanation-of-abstract-factory-design-pattern)

### 1.7 Builder Design Pattern
- [Explanation of the Builder Design Pattern](#explanation-of-the-builder-design-pattern)

### 1.8 Adapter Design Pattern
- [Explanation of Adapter Design Pattern](#explanation-of-adapter-design-pattern)

### 1.9 Circuit Breaker Design Pattern
- [Explanation of Circuit Breaker Design Pattern](#explanation-of-circuit-breaker-design-pattern)
- [States of the Circuit Breaker pattern](#states-of-the-circuit-breaker-pattern)
- [How to use Resilience4j in Spring Boot for Circuit Breaker](#how-to-use-resilience4j-in-spring-boot-for-circuit-breaker)

### 1.10 Saga Design Pattern
- [Explanation of the Saga Design Pattern](#explanation-of-the-saga-design-pattern)

---

## 2. System Design

### 2.1 Queue and Stack Data Structures
- [Explanation of Queue and Stack Data Structures](#explanation-of-queue-and-stack-data-structures)

### 2.2 Producer and Consumer Problem
- [Best data structures to solve the Producer and Consumer problem](#best-data-structures-to-solve-the-producer-and-consumer-problem)

### 2.3 Load Balancer
- [How a Load Balancer works using Round Robin](#how-a-load-balancer-works-using-round-robin)

### 2.4 Auto Scaling
- [Explanation of Auto Scaling in cloud infrastructure](#explanation-of-auto-scaling-in-cloud-infrastructure)

### 2.5 Distributed Tracing
- [How to implement a Distributed Tracing server and trace transactions](#how-to-implement-a-distributed-tracing-server-and-trace-transactions)

### 2.6 Monitoring Application Health
- [How to monitor the health of an application and retrieve metrics](#how-to-monitor-the-health-of-an-application-and-retrieve-metrics)

### 2.7 Microservices Architecture
- [Key components of a global microservices application](#key-components-of-a-global-microservices-application)
    - Spring Cloud Config Server
    - Service Discovery
    - API Gateway
    - Distributed Tracing Server
    - Circuit Breaker / Fault Tolerance
    - Load Balancer

### 2.8 Subscription Service Design
- [Design a subscription service and relevant questions](#design-a-subscription-service-and-relevant-questions)

---

## 3. System Design Projects

### 3.1 TinyURL (URL Shortener) System Design
- [Draw the design using tools like draw.io](#draw-the-design-using-tools-like-drawio)
- [Character size and encoding](#character-size-and-encoding)
    - ASCII vs UTF-8 vs UTF-16
- [Database Design (SQL or NoSQL, data saved, size per record)](#database-design-sql-or-nosql-data-saved-size-per-record)
- [How to scale the system](#how-to-scale-the-system)
- [Algorithms to shorten URLs](#algorithms-to-shorten-urls)
- [How base64 encoding works](#how-base64-encoding-works)
- [Ensuring uniqueness of the shortened URL](#ensuring-uniqueness-of-the-shortened-url)
- [How indexes work in SQL and their time complexity](#how-indexes-work-in-sql-and-their-time-complexity)
- [Sharding vs Partitioning](#sharding-vs-partitioning)

### 3.2 Retail Product Advertisement Add-on Service
- [Design the architecture for an add-on service allowing users to advertise purchased products](#design-the-architecture-for-an-add-on-service-allowing-users-to-advertise-purchased-products)

---

## 4. Performance Optimization

### 4.1 Handling Large Requests in Payment Services
- [How to reduce CPU usage and manage a large number of requests to return responses or errors efficiently](#how-to-reduce-cpu-usage-and-manage-a-large-number-of-requests-to-return-responses-or-errors-efficiently)

---

## 5. Design Patterns in Projects
- [What design patterns have been used in projects (Singleton, Factory, Builder, etc.)](#what-design-patterns-have-been-used-in-projects-singleton-factory-builder-etc)

---

## 6. Miscellaneous Topics

### 6.1 Strangler Design Pattern
- [What are the drawbacks of the Strangler Design Pattern?](#what-are-the-drawbacks-of-the-strangler-design-pattern)

### 6.2 API Design Patterns
- [Explanation of various API design patterns](#explanation-of-various-api-design-patterns)

### 6.3 Sharding vs Partitioning
- [Explanation of Sharding vs Partitioning](#explanation-of-sharding-vs-partitioning)

### 6.4 Singleton and Static Design Patterns
- [Difference between Singleton and Static Design Patterns](#difference-between-singleton-and-static-design-patterns)

---

**Note:** The above sections contain links to each topic for easy navigation. You can click on the links to dive into detailed explanations and implementations for each design pattern and system design concept.

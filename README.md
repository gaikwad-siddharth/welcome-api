# Welcome-API

Welcome-API is a Spring Boot microservice that exposes a **Welcome REST API**. It uses **Spring Cloud OpenFeign** to communicate with the **GREET-API** microservice and is integrated with **Spring Boot Actuator** and **Spring Boot Admin** for monitoring and management.

---

## Features

- RESTful Welcome API
- Inter-service communication using Spring Cloud OpenFeign
- Spring Boot Actuator for monitoring
- Spring Boot Admin Client integration
- Service discovery compatible (Eureka)
- Simple and scalable microservices architecture

---

## Tech Stack

- Java 17+
- Spring Boot
- Spring Cloud OpenFeign
- Spring Boot Actuator
- Spring Boot Admin Client
- Spring Cloud Netflix Eureka Client
- Maven

---

## Project Structure

```
src
 ├── main
 │   ├── java
 │   │   └── in
 │   │       └── siddharth
 │   │           ├── feign
 │   │           │     └── GreetFeignClient.java
 │   │           ├── rest
 │   │           │     └── WelcomeRestController.java
 │   │           └── WelcomeApiApplication.java
 │   └── resources
 │         └── application.yml
 └── test
```

---

## Application Configuration

### `application.yml`

```yaml
spring:
  application:
    name: Welcome-API

  boot:
    admin:
      client:
        url: http://localhost:1111/

server:
  port: 9091

management:
  endpoints:
    web:
      exposure:
        include: "*"
```

### Configuration Details

| Property | Description |
|----------|-------------|
| `spring.application.name` | Name of the microservice |
| `spring.boot.admin.client.url` | URL of the Spring Boot Admin Server |
| `server.port` | Application runs on port **9091** |
| `management.endpoints.web.exposure.include` | Exposes all Actuator endpoints |

---

## REST API

### Welcome Endpoint

**Request**

```
GET /welcome
```

**Example**

```
http://localhost:9091/welcome
```

**Sample Response**

```
Hello, Good Morning, Welcome To Spring Boot
```

---

## How It Works

1. Client sends a request to `/welcome`.
2. `WelcomeRestController` receives the request.
3. `GreetFeignClient` invokes the `/greet` endpoint of the `GREET-API`.
4. GREET-API returns a greeting message.
5. Welcome-API appends **", Welcome To Spring Boot"** and returns the final response.

### Request Flow

```
Client
   |
   | GET /welcome
   v
Welcome-API
   |
   | OpenFeign Client
   | GET /greet
   v
GREET-API
   |
   | "Hello, Good Morning"
   v
Welcome-API
   |
   | "Hello, Good Morning, Welcome To Spring Boot"
   v
Client
```

---

## Actuator Endpoints

All Spring Boot Actuator endpoints are exposed.

| Endpoint | Description |
|----------|-------------|
| `/actuator` | Lists all available endpoints |
| `/actuator/health` | Application health |
| `/actuator/info` | Application information |
| `/actuator/metrics` | JVM and application metrics |
| `/actuator/env` | Environment properties |
| `/actuator/beans` | Spring Beans |
| `/actuator/mappings` | Request mappings |
| `/actuator/loggers` | View and change log levels |
| `/actuator/threaddump` | Thread dump |
| `/actuator/heapdump` | Heap dump |

Example:

```
http://localhost:9091/actuator/health
```

---

## Spring Boot Admin

This application automatically registers itself with the Spring Boot Admin Server.

**Admin Server URL**

```
http://localhost:1111/
```

Once registered, you can monitor:

- Application Health
- JVM Metrics
- Memory Usage
- Environment Variables
- Request Mappings
- Spring Beans
- Threads
- Loggers

---

## Prerequisites

Before running the application, ensure the following services are available:

- Eureka Server (if using service discovery)
- GREET-API
- Spring Boot Admin Server
- Java 17+
- Maven 3.8+

---

## Build the Project

```bash
mvn clean install
```

---

## Run the Application

Using Maven:

```bash
mvn spring-boot:run
```

Or using the generated JAR:

```bash
java -jar target/Welcome-API.jar
```

---

## Required Dependencies

- Spring Boot Starter Web
- Spring Cloud OpenFeign
- Spring Boot Starter Actuator
- Spring Boot Admin Starter Client
- Spring Cloud Netflix Eureka Client

---

## Testing

Using a browser:

```
http://localhost:9091/welcome
```

Using cURL:

```bash
curl http://localhost:9091/welcome
```

Expected Response:

```
Hello, Good Morning, Welcome To Spring Boot
```

---

## Author

**Siddharth**

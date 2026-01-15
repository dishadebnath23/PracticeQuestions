Practice Questions – Day 9  
Microservices Framework

------------------------------------------------------------

1. How do microservices communicate with each other in a Spring Boot–based system?

Microservices mainly communicate using **HTTP-based REST APIs**.  
Each microservice exposes endpoints, and other services consume them.

Communication can be:
- Synchronous (REST calls)
- Asynchronous (Kafka / message brokers)

In Spring Boot, communication is commonly done using:
- RestTemplate
- WebClient
- Feign Client

------------------------------------------------------------

2. Difference between RestTemplate, WebClient, and Feign Client

| Feature        | RestTemplate            | WebClient                  | Feign Client                 |
|---------------|-------------------------|----------------------------|-------------------------------|
| Type          | Synchronous             | Asynchronous / Reactive    | Declarative REST client       |
| Blocking      | Yes                     | No                         | Depends on underlying client  |
| Code style    | Verbose                 | Functional / Reactive      | Very simple                   |
| Recommended   | No (deprecated)         | Yes                        | Yes (Spring Cloud)            |

Key understanding:
- RestTemplate is older and blocking
- WebClient is non-blocking and reactive
- Feign Client reduces boilerplate code and is easier to use

------------------------------------------------------------

3. How is a Feign Client integrated in a Spring Boot application?

a) Add dependency  
Spring Cloud OpenFeign dependency is added to the project.

b) Enable Feign  
Feign is enabled using:
- `@EnableFeignClients`

c) Create Feign interface  
An interface is created using:
- `@FeignClient(name = "service-name")`

Inside the interface, REST methods are defined using:
- `@GetMapping`
- `@PostMapping`

Spring Boot automatically generates the implementation at runtime.

------------------------------------------------------------

4. What happens if the called service is down?  
How do you handle failures?

If the called service is down:
- Requests fail
- Response time increases
- Cascading failures may occur

Failures are handled using:
- Circuit Breaker
- Retry mechanism
- Fallback methods
- Timeouts

Libraries like **Resilience4j** are commonly used for this.

------------------------------------------------------------

5. When would you prefer asynchronous communication instead of REST?  
How do you integrate Kafka in Spring Boot?

Asynchronous communication is preferred when:
- High throughput is required
- Services should not wait for responses
- Event-driven architecture is used

Kafka integration steps:
1. Add Kafka dependency
2. Configure Kafka broker details
3. Create producer and consumer
4. Use topics for communication

Kafka improves scalability and fault tolerance.

============================================================

6. How is configuration managed across multiple microservices?

Configuration is managed using:
- External configuration files
- Centralized configuration server
- Environment-specific properties

Each microservice reads its configuration at runtime.

------------------------------------------------------------

7. Why should configuration be externalized in microservices?

Configuration should be externalized because:
- Code should not change for config updates
- Same build can be deployed across environments
- Easier maintenance and scalability

This follows the **12-factor app principle**.

------------------------------------------------------------

8. How does Spring Cloud Config help in centralized configuration management?

Spring Cloud Config:
- Stores configuration in a central repository (Git/GitHub)
- Provides configuration to all microservices
- Supports environment-based configs

All services fetch configuration from the config server at startup.

------------------------------------------------------------

9. What happens when a configuration value changes?  
Do you need to restart services?

By default:
- Yes, services need restart

With Spring Cloud:
- `@RefreshScope` can be used
- Actuator `/refresh` endpoint refreshes config
- No restart required

------------------------------------------------------------

10. How do you manage environment-specific configurations (dev, test, prod)?

This is handled using:
- Separate config files
- Profiles (spring.profiles.active)
- Environment-based Git config files

Example:
- application-dev.yml
- application-test.yml
- application-prod.yml

============================================================

11. How do microservices discover each other dynamically?

Microservices use **Service Discovery** to find each other dynamically.

Instead of IP addresses:
- Services use service names
- Discovery server manages mappings

------------------------------------------------------------

12. What is the role of a service registry like Eureka?

Eureka:
- Acts as a service registry
- Maintains list of running services
- Handles dynamic IPs and scaling

------------------------------------------------------------

13. How does a service register itself with Eureka?

Steps:
1. Add Eureka Client dependency
2. Configure Eureka server URL
3. Enable client using `@EnableEurekaClient`

Service automatically registers on startup.

------------------------------------------------------------

14. How does a client service locate another service without knowing its IP?

Client service:
- Uses service name
- Eureka resolves the name to an instance
- Load balancer selects one instance

This removes hardcoded IPs.

------------------------------------------------------------

15. What issues occur if service discovery is not used?

Problems include:
- Hardcoded IP addresses
- Poor scalability
- Manual configuration
- High maintenance

============================================================

16. What is the circuit breaker pattern, and why is it used?

Circuit breaker prevents repeated calls to a failing service.

It improves:
- System stability
- Fault tolerance
- Response time

------------------------------------------------------------

17. How does a circuit breaker work internally?

States:
- Closed → normal operation
- Open → requests blocked
- Half-open → test requests allowed

Based on failure rate, state changes automatically.

------------------------------------------------------------

18. How is Resilience4j used in Spring Boot?

Resilience4j provides:
- Circuit breaker
- Retry
- Rate limiter
- Fallback methods

It is annotation-based and lightweight.

------------------------------------------------------------

19. Difference between retry and fallback mechanisms

Retry:
- Re-attempts failed requests
- Useful for temporary failures

Fallback:
- Executes alternative logic
- Used when service is unavailable

------------------------------------------------------------

20. Can retry cause problems if used incorrectly?

Yes, retry can cause:
- Increased load
- Network congestion
- Cascading failures

Retries must be limited.

------------------------------------------------------------

21. Should microservices share the same database? Why or why not?

No, microservices should not share databases.

Reasons:
- Tight coupling
- Independent scaling becomes difficult
- Data ownership issues

Each service should own its database.

============================================================

22. What is an API Gateway, and why is it used?

API Gateway:
- Entry point for all clients
- Routes requests to services

It simplifies client communication.

------------------------------------------------------------

23. What responsibilities does an API Gateway handle?

Responsibilities include:
- Routing
- Authentication
- Authorization
- Rate limiting
- Logging

------------------------------------------------------------

24. What problems occur if each microservice is exposed directly?

Problems:
- Security risks
- Client complexity
- Duplicate logic
- Poor maintainability

------------------------------------------------------------

25. Have you heard of Spring Cloud Gateway? What is it used for?

Spring Cloud Gateway:
- API Gateway implementation
- Built on reactive stack
- Supports filters and routing

It is commonly used in Spring Boot microservices.

------------------------------------------------------------

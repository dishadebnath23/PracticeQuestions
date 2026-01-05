Practice Questions – Day 5 (Spring Boot Fundamentals)

This document contains my practice answers for Day 5, focusing on Spring Boot fundamentals such as auto-configuration, dependency injection, profiles, configuration management, scheduling, and Actuator. The explanations are written in simple language and aligned with real-world and interview expectations.

Q1. You are migrating a legacy monolithic application to a microservice-based architecture using Spring Boot.

How does auto-configuration simplify bean creation compared to manual XML configurations?

Earlier, in traditional Spring applications, beans were defined and wired manually using large XML configuration files. This required explicit configuration for components like DataSource, transaction managers, and web components.

Spring Boot simplifies this using auto-configuration. Based on the classpath, starter dependencies, and application properties, Spring Boot automatically creates and configures beans. For example, adding spring-boot-starter-data-jpa automatically configures DataSource, EntityManager, and transaction management without writing XML.

The @SpringBootApplication annotation combines @Configuration, @EnableAutoConfiguration, and @ComponentScan, which enables this behavior.

Auto-configuration uses conditional annotations such as @ConditionalOnClass and @ConditionalOnMissingBean to provide default beans while still allowing customization.

When would you exclude an auto-configuration class? Give an example.

An auto-configuration class is excluded when we want full control over a particular configuration. For example, if we want to configure a custom DataSource instead of the default one provided by Spring Boot, we can exclude DataSourceAutoConfiguration.

Example:
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)

How do you activate profile-specific beans?

Profile-specific beans are activated using the @Profile annotation. Profiles can be enabled using the spring.profiles.active property in application.yml, application.properties, or via environment variables.

Example:
@Profile("dev")
@Component
class DevBean {
}

Q2. Can you explain these concepts in Spring Boot?

What is Dependency Injection (DI), and how does it reduce coupling?

Dependency Injection is a design principle where objects receive their dependencies from the framework instead of creating them directly. This reduces tight coupling between classes, improves testability, and makes the application easier to maintain and extend.

Explain the roles of common annotations and how component scanning discovers them.

@Component is a generic stereotype annotation for any Spring-managed component.

@Service is used in the service layer to indicate business logic.

@Repository is used in the persistence layer and also enables exception translation for database operations.

@Controller is used for MVC controllers that return views.

@RestController is used for REST APIs and automatically serializes responses into JSON.

Spring uses component scanning to automatically detect these annotated classes and register them as beans.

When would you use @Autowired vs constructor injection? Why is constructor injection preferred?

@Autowired can be used for field or constructor injection. Constructor injection is preferred because it makes dependencies explicit, ensures immutability, and allows easier unit testing. It also avoids issues related to partially initialized objects.

How do @Qualifier and @Primary help resolve bean ambiguity?

When multiple beans of the same type exist, Spring cannot decide which one to inject.

@Primary marks one bean as the default choice.

@Qualifier is used to explicitly specify which bean should be injected.

Example:
@Qualifier("mysqlDataSource")
@Autowired
private DataSource dataSource;

Q3. Your team needs to externalize secrets and rotate them without redeploying the app.

How do application.yml and profile-specific configs work together?

application.yml contains common configuration shared across environments. Profile-specific files like application-dev.yml or application-prod.yml override or extend these properties based on the active profile.

This allows different configurations for different environments without changing code.

What’s a secure approach for managing secrets in Spring Boot?

Secrets should not be stored directly in source code or configuration files. A secure approach is to use environment variables, external configuration servers, or secret management tools like Vault or cloud secret managers.

How would you structure configs for multi-region deployments?

For multi-region deployments, common configs can be placed in application.yml, while region-specific configurations can be handled using profiles such as application-us.yml or application-eu.yml. Environment variables can also be used for region-specific overrides.

Q4. A batch job must run every 10 seconds and stop gracefully during scale-down.

Which annotations enable scheduling? How do you restrict it to certain profiles?

Scheduling is enabled using the @EnableScheduling annotation, and tasks are defined using @Scheduled.

To restrict scheduling to certain profiles, the @Profile annotation can be used on the scheduled component.

Which lifecycle hooks help with graceful shutdown?

Graceful shutdown can be handled using @PreDestroy or implementing DisposableBean. These hooks allow cleanup logic to run before the application stops.

Which Actuator endpoints help monitor this job?

Spring Boot Actuator provides endpoints such as /actuator/health, /actuator/metrics, and /actuator/loggers, which can be used to monitor application health, job execution metrics, and runtime behavior.

1. The main goal of Spring Boot is to quickly create Spring-based applications without requiring developers to write the same boilerplate configuration again and again.
2. Spring Boot key features-
	1. Spring boot starters
	2. Spring boot `auto-configuration`
	3. Elegant configuration management
	4. Spring boot `actuator`
	5. Easy-to-use embedded `servlet` container support
3. SB configures various components automatically by registering beans based on various criteria-
	1. availability of a particular class in a classpath
	2. presence or absence of a spring bean
	3. presence of a system property
	4. absence of a configuration file
4. SB supports externalizing configurable properties using the `@PropertySource` configuration
5. Spring Boot `actuator` feats-
	1. can view the application bean configuration details
	2. can view the application URL mappings, environment details and configuration parameter values
	3. can view the registered health check metrics
6. By inheriting from `spring-boot-starter-parent` module the new module will automatically have these feats-
	1. only need to specify the SB version once in the parent module configuration
	2. already includes the most commonly used plugins, such as `maven-jar-plugin`, `maven-surefire-plugin`, `maven-war-plugin`, `exec-maven-plugin` and `maven-resources-plugin` with sensible defaults
7. also configures the `spring-boot-maven-plugin` which is to build fat JARs
8. `@SpringBootApplication = @SpringBootConfiguration + @EnableAutoConfiguration + @ComponentScan + others`
   ![[Pasted image 20250127173420.png]]
9. `@SpringBootConfiguration = @Configuration + others`
10. `@Configuration` - indicates that the class is a Spring configuration class
11. `@ComponentScan` - enables component scanning for Spring beans in the package in which the current class is defined
12. `@EnableAutoConfiguration` - triggers SB's auto-configuration mechanism
13. Bootstrapping an SB application by calling `SpringApplication.run(App.class, args)` inside the `main()` method.
14. By default, SB serves the static content from the `src/main/public/` and `src/main/static/` directories
15. Spring Boot applications should have an entry point class with the `public static void main(String[]args)` method, which is usually annotated with the `@SpringBootApplication` annotation and will be used to bootstrap the application.
16. Highly recommended that the main entry point class be in the root package so that the `@EnableAutoConfiguration` and `@ComponentScan` annotations will scan for Spring beans, JPA entities etc in the root and all of its sub-packages automatically.
17. If an entry point class in a nested package, it is needed to specify the `basePackages` to scan for Spring components explicitly.
18. `@ComponentScan` - for scanning spring components
19. `@EntityScan` - for scanning spring data JPA entities

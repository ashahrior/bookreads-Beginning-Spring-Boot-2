1. Spring Boot, by default, includes `spring-boot-starter-logging` as a transitive dependency for the `spring-boot-starter` module.
2. By default, Spring Boot includes `SLF4J` along with `Logback` implementations.
3. Spring Boot has a `LoggingSystem` abstraction that automatically configures logging based on the logging configuration files available in the classpath.
4. logging levels configuration can be done withing the `application.properties` file
5. If the `logback.xml` file is placed in the root classpath, SB will automatically use it to configure the logging system
6. Spring provides the `@PropertySource` annotation to specify the list of configuration files
7. SB automatically registers a `PropertyPlaceHolderConfigurer` bean using `application.properties` file in the root classpath by default
8. Profile specific configuration files can be created using the filename as `application-{profile}.properties`. e.g. *application-dev.properties, application-prod.properties, application-default.properties*
9. Spring provides `@Value` annotation to bind any property value to bean property
10. Annotate a class with `@ConfigurationProperties(prefix="jdbc")` to automatically bind properties
11. **Relaxed Binding** - The bean property names need not be exactly the same as the property key names. Spring Boot supports relaxed binding, where the bean property `driverClassName` will be mapped from any of these: *driverClassName, driver-class-name, or DRIVER_CLASS_NAME.*
12. There are **Bean Validation API** annotations such as `@NotNUll`, `@Min`, `@Max`, etc. to validate the property's value
13.  Spring Boot provides developer tools (the `spring-boot-devtools` module) that include support for quick application restarts whenever the application classpath content changes.
14. When the `spring-tool-devtools` module is included during development, the caching of the view templates (e.g. *thymeleaf, velocity, freemarker,* etc) will be disabled automatically so the changes can be seen immediately. Whenever you change the class or properties files in the classpath, Spring Boot will automatically restart the server. 
16. with  `<optional>true</optional>`, the `spring-boot-devtools` won't be packaged in a fat JAR. 
```xml
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-devtools</artifactId>
<optional>true</optional>
</dependency>
```

17. Once you configure `spring.devtools.restart.trigger-file` and update the trigger file, the server will restart only if there are modifications to the files being watched. Otherwise, the server won’t be restarted.
18. The restart mechanism works by using two `classloaders`—one (the *base classloader*) to load *classes that don’t change* (such as classes in third-party jars) and the other (the *restart classloader*) to load *classes that frequently change* (such as classes from your application code). When the application restarts, only the classes in the restart classloader will be recreated. This will yield faster restarts.

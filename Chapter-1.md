1. Spring at its core is a **dependency injection container** that provides **flexibility to configure beans** in multiple ways
2. Spring boot configures applications automatically but leaves scope for overriding defaults
3. `springboot-starter-web` dependency-
	1. adds libraries such-
		1. spring-webmvc
		2. jackson-json
		3. validation-api
		4. tomcat - pulls `spring-boot-starter-tomcat` automatically
	2. configures the commonly registered `beans` like-
		1. `DispatcherServlet`
		2. `ResourceHandlers`
		3. `MessageSource`
4. `spring-boot-starter-thymeleaf` adds the `Thymeleaf` library dependencies and configures the `ThymeleafViewResolver` beans
5. If there's any in-memory database drivers like `H2` or `HSQL` in the classpath, then Spring Boot will automatically create and in-memory datasource and will register the `EntityManagerFactory` and `TransactionManager` beans automatically with sensible defaults.
6. In case of using actual database, the connection details are configured inside the `application.properties` file and spring boot creates a `DataSource` using those properties.
7. Inside the `main()` method, it starts the `tomcat` server as an embedded container so that there is no need for deployment on any externally installed tomcat server.

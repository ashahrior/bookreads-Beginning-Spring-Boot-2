1. `spring-boot-starter-jdbc` module for using `JdbTemplate` which bring the following features-
	1. `spring-boot-starter-jdbc` module transitively pulls `tomcat-jdbc-{version}.jar` which is used to configrue the `DataSource` bean
	2.  If `DataSource` bean not defined explicitly and there's any embedded database drivers in the classpath, such as *H2, HSQL,* or *Derby*, then Spring Boot will automatically register the `DataSource` bean using the *in-memory database settings*.
	3.  If none of the following beans have been registered, then SB will register them automatically.
		 • `PlatformTransactionManager (DataSourceTransactionManager)`
		 • `JdbcTemplate`
		 • `NamedParameterJdbcTemplate`
	 4. Let the `schema.sql` and `data.sql` files in the `root` classpath, which Spring Boot will automatically use to initialize the database.
2. Spring Boot uses the `spring.datasource.initialize` property value, which is true by default, to determine whether to initialize the database
3. SB, by default, pulls in `tomcat-jdbc-{version}.jar` and uses `org.apache.tomcat.jdbc.pool.DataSource` to configure  the `DataSource` bean
4. `Flyway` - a popular database migration tools that SB supports out of the box
                    
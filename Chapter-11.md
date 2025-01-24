1. **REST** stands for `Representational State Transfer` and is an architectural style for designing distributed hypermedia systems.
2. Following the REST principles, these are the following `HTTP` verbs-
	1. `GET` - to get a collection or a single resource
	2. `POST` - to create a new resource
	3. `PUT` - to update an existing resource
	4. `DELETE` - to delete a collection or a single resource
3. The typical practice of determining the input request content and output response types in web based systems are based on the `ContentType` and `Accept` header values
4. The `@ResponseBody` annotation on the request handler method indicates that the return value should be bound to response body
5. The `@RequestBody` annotation will take care of binding the web request body to the method parameters with the help of the registered `HttpMessageConverter`s. So when a `POST` request is made to some URL with a JSON body, `HtppMessageConverter` converts the JSON request body into `<class>` object
6. `@RestController = @Controller + @ResponseBody`
   ```mermaid
   graph TD
    A[@Controller] --> C[@RestController]
    B[@ResponseBody] --> C[@RestController]
	```

7. In addition to returning an arbitrary object from request handler methods, it is possible to return `RequestEntity/HttpEntity`, which provides an easy way to set *response headers* and the *status code*

### CORS (Cross-Origin Resource Sharing) support
1. For security reasons, browsers don't allow it to make AJAX requests to resources residing outside of the current origin.
2. CORS specification provides a way to specify which cross-origin requests are permitted
3. Spring MVC provides support for enabling CORS for REST API endpoints so that the API consumers, such as web clients and mobile devices, can make calls to REST APIs.
4. Enable CORS at the controller level or at the method level using the `@CrossOrigin` annotation
5. CORS support enables method using default configuration-
	1. All headers and origins are permitted
	2. Credentials are allowed
	3. Maximum age is set to 30 minutes
	4. The list of HTTP methods is set to the methods on the `@RequestMethod`annotation
6. Apart from being specified at class and method level, CORS can be configured globally by implementing the `WebMvcConfigurer.addCorsMappings()` method
7. Possible to specify `allowedOrigins("*")` to allow requests from any origin

### Exposing JPA Entities with Bi-Directional References through RESTful Services
1. When trying to [marshal](https://docs.redhat.com/en/documentation/red_hat_data_grid/7.1/html/performance_tuning_guide/marshalling#marshalling-1) a JPA parent entity that has a collection of child entities and the child has a reference back to the parent, then the JPA marshaling will end up in infinite recursion and will throw `StackOverflowError`
2. SB by default configures the JSON library to marshal/unmarshal java beans into JSON and vice versa
3. `@JsonIgnore` - to break the infinite recursion by adding the `@JsonIgnore` annotation on the back reference from the child object
4. `@JsonIgnoreProperties` - can be used at the class level to list all the property names to ignore
5. `@JsonManagedReference` and `@JsonBackReference` - are used to break the infinite recursion as well
6. `@JsonManagedReference` - annotation is used to indicate that the annotated property is part of a two-way linkage between fields and that its role is as a *"parent"* (or *"forward"*) link.
7. `@JsonBackReference` - annotation is used to indicate that the associated property is part of a two-way linkage between fields and its role is as a *"child"* (or *"back"*) link
8. Java Object Mapper libraries to provide data abstraction via Data Transfer Objects (DTOs) with- Dozer, [ModelMapper](https://modelmapper.org/), MapStruct

### REST API using Spring Data REST
1. Spring Data REST builds on top of the Spring Data repositories and automatically exports them as REST resources
2. SB will automatically enable Spring Data REST if `spring-boot-starter-data-rest` is added to the application `pom.xml`
3. If the Repository extends `PagingAndSortingRepository`, then Spring Data REST endpoints support pagination and sorting out-of-the-box. `size` query can be used to limit the number of entries returning. Use `page`, `size`, `sort` parameters.
4. Spring Data REST by default exposes all the public repository interfaces without requiring any extra configuration. 
5. One can disable specific methods from being exposed as REST resources by adding `@RestResource(exported=false)` on the methods
6. `spring.data.rest.*` - to customize various properties inside the `application.properties` file
7. Enable **CORS** support for Spring Data REST endpoints using the `@CrossOrigin `annotation at the repository level . To enable support globally, extend `RepositoryRestConfigurerAdapter` and provide CORS configuration

### Exception Handling
1. `@ExceptionHandler` methods and `@ControllerAdvice` class- combination of these to handle exceptions globally
2. Controller level exception handling-
   ![[Pasted image 20250124153125.png]]
3. Global exception handling-
   ![[Pasted image 20250124153204.png]]
	The global exception handling mechanism helps to handle exceptions in a central place instead of handling them in each controller class.

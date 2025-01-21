1. Spring Boot eases Spring MVC initiation process via autoconfiguration mechanism to configure these various web layer components-
	1. `DispatcherServlet`
	2. `ViewResolvers`
	3. `ContentNegotiatingViewResolver`
	4. `LocaleResolver`
	5. `HandlerExceptionResolver`
	6. `MessageCodesResolver`, etc.

2. Spring MVC `DispatcherServlet` - 
	1. acts as a front controller
	2. receives all the requests
	3. delegates the processing to request handlers (controllers)
3. `ViewResolver` - renders a view based on the view name after the processing is done
4. `SpringMVC ` request processing flow-
   ![[Pasted image 20250120142611.png]]
5. Spring MVC provides *annotation-based mapping* support to map request URL patterns to handler classes using `@Controller` and `@RequestMapping` annotations
6. `@Controller` - marks a class as a request handler Spring component
7. `ViewResolver` - resolves the logical view name to a view template and render the view
8. SB Web starter `spring-boot-starter-web` for developing web applications using Spring MVC
9. JAR type module using an embedded servlet container
10. WAR type module that can be deployed on any external servlet container
11. The `spring-boot-starter-web` starter by default-
   1. configures `DispatcherServlet` to the URL pattern `"/"`
   2. adds `Tomcat` as the embedded servlet container which runs on port 8080
12. SB by default serves the static resources (HTML, CSS, JS, images, etc.) from the following `CLASSPATH` locations-
   1. `/static`
   2. `/public`
   3. `/resources`
   4. `/META-INF/resources`
   5. Possible to override the static resources locations by configuring the `spring.resources.staticLocations` property in the `application.properties`
	      > spring.resources.staticLocations=classpath:/assets/

13. By default SB web starter uses Tomcat as the embedded servlet container and runs on port `8080`. But this can be customized inside the `application.properties` file with `server.*` prefix
14. `ThymeleafAutoConfiguration` takes care of registering 
   1. `TemplateResolver`, 
   2. `ThymeleafViewResolver`, 
   3. `SpringResourceTemplateResolver`, and 
   4. `SpringTemplateEngine`
15. `@Valid` - annotation to the model parameter to perform validations on the form submit
16. Need to define the `BindingResult` parameter *immediately next to the model object.* The validation errors will be populated in `BindingResult`, which can be later inspected inside the method body. When the form is submitted with invalid data, those validation errors will be populated in `BindingResult`
```java
@Controller
public class RegistrationController
{
    ...
    ...
    @PostMapping("/registration")
    public String handleRegistration(@Valid User user, BindingResult result) {
        logger.debug("Registering User : "+user);
        if(result.hasErrors()){
            return "registration";
        }
        return "redirect:/registrationsuccess";
    }
}
```

17. Spring's validation framework to implement complex validations via implementing `org.springframework.validation.Validator` interface
18. It is possible to handle exceptions globally by creating an exception handler class annotated with `@ControllerAdvice`. The `@ExceptionHandler` methods in the `@ControllerAdvice` class handle errors that occur in any controller request handling method.
19. SB registers a global error handler and maps `/error` by default, which renders an HTML response for browser clients and JSON response for REST clients. 
20. It is possible to provide custom error page by implementing `ErrorController`

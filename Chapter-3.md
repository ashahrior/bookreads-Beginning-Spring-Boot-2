1. SB auto-configuration is heavily dependent on `@Conditional` feature
2. Spring introd *`profiles`* - can register multiple beans of the same type and associate them with one or more profiles. This approach works fine for simple cases where enabling-disabling beans based on activated profiles.
   ![[Pasted image 20250110003426.png]]
3.  To provide more flexibility, with `@Conditional` approach a bean can be conditionally registered based on arbitrary condition. For instance-
	1. A specific class is present in the classpath
	2. A spring bean of a certain type isn't already registered in the `ApplicationContext`
	3. A specific file exists in a location
	4. A specific property value is configured in a configuration file
	5. A specific system property is present/absent
4. `@Conditional` can be used to register a bean-
	1. based on system properties
	2. based on presence/absence of java class
	3. based on the configured spring beans- create a condition to check if there are any existing beans of a certain type
	4. based on a property's configuration - register beans if some property is set in the property's placeholder configuration file
5. An example-
   ![[Pasted image 20250110013637.png]]
   ![[Pasted image 20250110013718.png]]

**Spring Boot @Conditional Annotations**

| Annotation                   | Description                                                                      |
| ---------------------------- | -------------------------------------------------------------------------------- |
| @ConditionalOnBean           | Matches when the specified bean classes and/or names are already registered.     |
| @ConditionalOnMissingBean    | Matches when the specified bean classes and/or names are not already registered. |
| @ConditionalOnClass          | Matches when the specified classes are on the classpath.                         |
| @ConditionalOnMissingClass   | Matches when the specified classes are not on the classpath.                     |
| @ConditionalOnProperty       | Matches when the specified properties have a specific value.                     |
| @ConditionalOnResource       | Matches when the specified resources are on the classpath.                       |
| @ConditionalOnWebApplication | Matches when the application context is a web application-context.               |

 **How SB Autoconfiguration Works**
 1. The key to SB's autoconfiguration is its `@EnableAutoConfiguration` annotation.
 2. The `@EnableAutoConfiguration` annotation enables the autoconfiguration of Spring `ApplicationContext` by scanning the classpath components and registering the beans that match various conditions.
 3. `Autoconfiguration` classes are typically annotated with `@Configuration` to mark it as a `Spring configuration class` and annotated with `@EnableConfigurationProperties` to bind the customization properties and one or more conditional bean registration methods.
 4. Bean definitions are registered in `ApplicationContext` only if conditions match
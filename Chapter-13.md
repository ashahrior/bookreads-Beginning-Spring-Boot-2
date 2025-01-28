1. Authentication is the process of verifying the user, which is typically done by asking for credentials.
2. Authorization is the process of verifying whether or not the user is allowed to do a certain activity.
3. Spring Security can be used to secure non-spring-based web applications as well.
4. Adding the Spring Security Starter (`spring-boot-starter-security`) to an SB application will-
	1. Enable HTTP basic security
	2. Register the `AuthenticationManager` bean with an in-memory store and a single user
	3. Ignore paths for commonly used static resource locations (such as `/css/**`,  `/js/**`, `/images/**`, etc.)
	4. Enable common low level features such as XSS, CSRF, caching, etc.
5. 
# Spring Security
## 1. Definition
- Framework
- 2 basic standard:
	+ Authentication: customize a `Principal` -> authen if it is allowed to access the application -> login using username and password
	+ Authorization (access-control): need the `Principal` of Authentication. -> match the role
### 2. Dependency
```
<!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-core -->
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.6.1</version>
</dependency>
```
All security dependencies must be the same versions.

### 3. Annotations
```
@EnableWebSecurity
```
Enable debug to see the numbers of needed filters go through our request
<br/> `@EnableWebSecurity(debug=true)` (not recommend to use)

### 4. Filter Chain
`SecurityInitializer.java` **implements** `AbstractSecurityWebApplicationInitializer` interface
`MySecurityConfig.java` **implements** `WebSecurityConfigurerAdapter`

- Flow come to `SecurityInitializer.java` first to register filter chain with our application
- Then `MySecurityConfig.java` will create a filter chain

**NOTICE:**
`DelegatingFilterProxy` helps to register your spring security filter chain (by calling a bean inside interface `WebSecurityConfiguration` to create the filter)
<br/> Flow: request -> `DelegatingFilterProxy` -> `FilterChainProxy` -> `SecurityFilterChain`-> `DispatcherServlet`



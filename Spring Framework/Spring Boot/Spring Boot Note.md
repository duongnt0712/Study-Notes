# SPRING BOOT
`Spring Boot` = `Spring Framework` + `Embedded HTTP Servers` - `XML Configuration or @Configuration`

## 1. Configuration
Use only `@SpringBootApplication` (replace `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`)

## 2. Application Properties
- Edit properties inside `application.properties`
- Usually set `server-port` or config `database connection`

## 3. Annotations
**HTTP**
-`@GetMapping`: fetches
-`@PostMapping`: create
-`@PutMapping`: create or updates
-`@DeleteMapping`: delete
-`@PatchMapping`
-`@RequestBody`: bind HTTP request with an object in method param
-`@ResponseBody`: bind the method return value to the response body
-`@PathVariable`: extract value from URI
-`@RequestParam`: extract query parameters from URL
-`@RequestHeader`: get the details about the HTTP request headers, use as method param
-`@RestController`: combination of `@Controller` and `@ResponseBody`
-`@RequestAttribute`: bind a method param to request attribute

## 4. AOP
- Additional technique for OOP
- Usually implement:
	+ Logging
	+ Exception Handling 
	+ Transaction Management

**Terminology**
- **Aspect**: a modularization of a concern that cut across multiple classes.
- **Join Point**: any point such as method execution, exeption handling, etc.
- **Advice**: represent an action taken by aspect at particular join point.
- **Pointcut**: expression of AOP that marches join point.

**Advice**
- Using **Joinpoint** for those advice types: `@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`
- Using `ProceedingJoinPoint` for `@Around`
- 5 types:
	+ `@Before`: 
	+ `@After`
	+ `@AfterReturning`: invokes after the execution of join point complete, does not invoke if an exception is thrown
	+ `@AfterThrowing(PointCut="execution(expression)", throwing="exception_name")`: run if a method throws an exception
	+ `@Around`: executes before and after a join point

## 5. Database
- JPA: standard approach for ORM
- JDBC
- H2

## 6. Thymeleaf
Server-side Template engine
- Variable expression: `${...}`
- Form backing bean: `*{...}`
- Hash expression: `#{...}`
- Rewrite URLs: `@{...}`

## 7. Cache
- Class-level: 
	+ `@EnableCaching`: in Spring Boot application
	+ `@CacheCongif(cacheNames={"..."})`: in class
- Method-level:
	+ `@Caching(evict={@CacheEvict(...)})`: group all `CacheEvict` annotations
	+ `@Cacheable(value="", key="", condition="")`: for method's return value, it skips the method execution
	+ `@CachePut(cacheNames="", key="")`: update cache without interfering method execution, it runs the method and put the result into the cache.
	+ `@CacheEvict()`: remove unused data from the cache

# SPRING CORE

## 1. IOC (Inversion of Control)
- Creating and manage object for us, helping our application be configurable and managing dependencies.
- Combine with `Dependency Injection`

- **IOC Container**: manage beans - create object, write them together, config and manage their life cycle till destruction.
		configuration metadata: XML, Java annotations, Java code.
	+ **BeanFactory**
	(use for lightweight application): provide config framework and basic function
	<br/>Ex: `XmlBeanFactory`
	+ **ApplicationContext** (recommend): extends from BeanFactory with more enterprise-specific functionality: resolve textual messages from a properties file, publish application events to interested event listeners.
	<br/>Common implementation: 
		`ClassPathXmlApplicationContext`
		`FileSystemXmlApplicationContext`		
		`WebXmlApplicationContext`
- **MainApp**:
	+ ApplicationContext: 
		- using `ClassPathXmlApplicationContext()`: load beans configuration file and take care of creating and initializing all objects (beans mentioned in config file)
		- using `AnnotationConfigApplicationContext()`: load to read config file
	+ use `getBean()` - use bean ID to return generic object, then cast to actual object.
	<br/>How to use: 	`(class_name) context.getBean("bean_name");`
			`context.getBean("bean_name", class_name.class)`
- **Bean Configuration File**: `Beans.xml`
```
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
	
	<bean id="" class=""></bean> //object
	<bean id="" class=""></bean>

</beans>
```
- **Benefits**: 
	+ minimize the amount of code
	+ make application easy to test (doesn't require any singletons in unit test cases.)
	+ IOC container support eager instantiation and lazy loading of services.

## 2. Dependency Injection (DI)
- Not create objects but describe how they should be created
- Not directly connect to components and services but describe which services are needed by which components in config file. 
IOC container is then responsible for hooking it all up.
- **2 types**:
	+ `Constructor-based DI`: container invokes a class constructor with arguments, each representing a dependency on other class, dont need setter.
	<br/>`<contructor-arg name="" value="" type=""/>`
	+ `Setter-based DI`: container call setter methods after invoking no-argument constructor or no-argument static factory method to instantiate bean.
	<br/>`<property name="" value=""/>`
	<br/>`<property name="" ref=""/>`
- **3 forms**:
	+ Injection literals
	+ Injection object
	+ Injection collection

## 3. Bean Scope
- Initiate bean:
```
<bean> id="name" class="link to class" scope="">
	<property name="var name" value="passed value" />
</bean>
```

- Using **Annotation**: initialize a bean
<br/>@Bean: use only inside `@Configuration`

- Scope: `singleton` | `prototype` | `request` | `session` | `application` | `websocket`

- How to: 
<br/>`@Component`
<br/>`@Scope(value="scope_name")`
	+ request, session, application, websocket: use for ApplicationContext impl ( `XMLWebApplicationContext` and `AnnotationConfigWebApplicationContext`)
	+ singleton: default scope, create only one instance each bean everytime a request has called.
	+ prototype: can create new instance everytime has new request.

## 4. Autowiring
- `@Autowired`: auto match value in container and inject without setting property value for bean.
<br/>4 autowired mode: no, byType, byName, constructor
<br/>or use: `<bean id="" class="" autowire="autowired_mode">`
<br/>Ex: 	`byName` - match the **ref bean id** with the **constant name** of this class.
	`byType` - match the **ref bean class** with **class name** 
	`constructor` - match the **ref bean** with the **constructor** of this class.
- Use via class filed, via a setter, via constructor(easy test)
- In Bean configuration, use `<context:annotation-config />` to turn on annotation wiring annotation.
- In case the autowired cannot match all the mode, use `@Qualifier("bean_id")` to specify before the dependency(class constant).
- No need to write setter and constructor when using `@Autowired` (and `@Qualifier`) before dependency.

## 5. Annotations
- `@Component("bean_id")`, `@Repository`(persistence layer), `@Service` (business layer), `@Controller` (presentation layer): all is a BEAN
<br/>`<context:component-scan base-package="package_path">`
- `@Configuration`: use for config files.
- `@ComponentScan`: scan bean if using `@Component`
- `@PropertySource(classpath:file_name.properties")`: when using properties file
- `@Import`: for loading `@Bean`
- LifeCycle Callback: `@Bean(initMethod="method_name", destroyMethod="method_name")`
- `@Scope("scope_name")`: default is `singleton`, can change to `prototype`, `session`, ... 

## 6. Dependencies
```
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-context</artifactId>
</dependency>
```
- Servlet Library: 
`http://mvnrepository.com/artifact/javax.servlet/javax.servlet-api`
- Spring dependencies: 
```
http://mvnrepository.com/artifact/org.springframework/spring-core
http://mvnrepository.com/artifact/org.springframework/spring-web
http://mvnrepository.com/artifact/org.springframework/spring-webmvc
https://mvnrepository.com/artifact/org.springframework/spring-jdbc
https://mvnrepository.com/artifact/mysql/mysql-connector-java
```

## 7. Event Handling 
- Provided through `ApplicatonListener<event_name>` interface, using `ConfigurableApplicationContext`
- Listen through method `onApplicationEvent()`
- Built-in Events:
	+ ContextRefreshedEvent: `refresh()`
	+ ContextStartedEvent: `start()`
	+ ContextStoppedEvent: `stop()`
	+ ContextClosedEvent: `close()`
	+ RequestHandledEvent: web-specific for HTTP request

## 8. AOP 
`Aspect-oriented programming`
- **Cross-cutting concern**: the functions that span multiple points of an application.
- A technique allow modularizing crosscutting concerns, or behavior that cut across the typical divisions of responsibility (logging, transaction managent)
- Core construct: aspect - encapsulates behaviors affecting multiple classes into reusable modules.

## 9. JDBC Framework
- Open connection, execute SQL statement, process exceptions, handle transactions, close connection
- Execute SQL statement
	+ `queryForInt()`
	+ `queryForLong()`
	+ `queryForObject()`
- Execute DDL statement: `execute(SQL)`
- **DataSource** class: `org.springframework.jdbc.datasource.DriverManagerDataSource`
- Query Basic:
```
SELECT * FROM table;
INSERT INTO table (var1,var2) VALUES (?,?);
UPDATE table SET var1=?, var2=? WHERE var3=?;
DELETE FROM table WHERE var=?;
```

## 10. Transaction Management
- An abstract layer on top of different underlying transaction management APIs.
- Defined by `PlatformTransactionManager` interface:
	+ `TransactionStatus getTransaction(TransactionDefinition definition)`
	+ `commit(TransactionStatus status)`
	+ `rollback(TransactionStatus status)`
- Local transaction specific to a single transactional resource
- Global transaction is required in a distributed computing environment where all the resources are distributed across multiple system.
- 2 types: 
	+ Programmatic: manage transaction with the help of program
	+ Declarative: separate transaction from business code

## 11. Web MVC Framework 
`Model - View - Controller`
- After receiving HTTP request, DispatcherServlet consults HandlerMapping to call Controller
- Controller take request and call service methods to return view name to DispatcherServlet
- DispatcherServlet will take help from ViewResolver to find the defined view for request
- Finally, DispatcherServlet pass model data to the view.

- Required Config: map request in `web.xml`
```
<servlet></servlet>
<servlet-mapping><servlet-mapping>
```

## 12. Customize a bean
- Initialization method after DI is done
<br/>`@PostConstruct`
- Destroy method to signal that the instance is in the process of being remove by the container, using `close()`(close permanently) or `registerShutdownHook()` (close temporary)
<br/>`@PreDestroy`
- Instead of using `<context:annotation-config/>`, using `<bean class="...context.annotation.CommonAnnotationBeanProcessor"></bean>`

## 13. Bean LifeCycle
- 3 ways to config life cycle methods in spring
	+ `Annotation Approach`
	+ `XML Approach`
	+ `Configuring bean life cycle` <br/>
	
(1) Custom bean as above part or <br/>
(2) controlled using `init()` method or <br/>
(3) using `InitializingBean`/`DisposableBean` interfaces **(NOT RECOMMENDED)**
```
org.springframework.beans.factory.InitializingBean
org.springframework.beans.factory.DisposableBean
```

Interface:	`ApplicationContext`
<br/>AbstractClass:	`AbstractApplicationContext`
<br/>Class:		`ClassPathXmlApplicationContext`

## 14. Inject from properties file 
- In Bean configuration, add `<context:property-placeholder location=" classpath:file_name.properties"/>` to define the properties file.
- Call inside <bean>: `<property name="" value="${properties_var}" />` <br />
or <br /> 
Use `@Value("value_here")` before setter methods (Add `@Required` above for mandatory constant) <br />
Ex: 	`@Value("Daibeodeptrai")` <br />
	`@Value("${cat.name}")` (which in properties file)

# RERFERENCE:
```
https://www.tutorialspoint.com/spring/index.htm
https://groupe-sii.github.io/cheat-sheets/spring/spring-core/index.html
https://www.youtube.com/playlist?list=PL3NrzZBjk6m-nYX072dSaGfyCJ59Q5TEi
```
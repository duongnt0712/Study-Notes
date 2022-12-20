#COMMON XML CONFIG

## 1. web.xml 
```
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
	 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
	http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
	version="3.0"> 

	<display-name></display-name>

	<servlet>
		<servlet-name></servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<load-on-startup>1</load-on-startup>
	</servlet>

	<servlet-mapping>
		<servlet-name></servlet-name>
		<url-pattern>/*</url-pattern>
	</servlet-mapping>
</web-app>
```

##  2. file_name-servlet.xml
```
<beans 	xmlns="http://www.springframework.org/schema/beans"
	    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	    xmlns:context="http://www.springframework.org/schema/context"
	    xmlns:mvc="http://www.springframework.org/schema/mvc"
	    xsi:schemaLocation="http://www.springframework.org/schema/beans
	    http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
	    http://www.springframework.org/schema/context
	    http://www.springframework.org/schema/context/spring-context-4.0.xsd
	    http://www.springframework.org/schema/mvc
	    http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd">  

	
</beans>
```

## 3. pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	
	<build>
		<plugins>
			<plugin>
	            		<groupId>org.apache.maven.plugins</groupId>
	            		<artifactId>maven-compiler-plugin</artifactId>
	            		<version>3.1</version>
	            		<configuration>
	                	<source>1.8</source>
	                	<target>1.8</target>
	            		</configuration>
	        	</plugin>
        	</plugins>
	</build>
</project>
```
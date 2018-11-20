### What does @SpringBootApplication annotation means?
1. It indicates that this is a spring context file.
2. It enables Auto Configuration.
3. It perform component scan.

### What would happen at the startup?
The spring freamework would trigger the auto-configuration jar. And, it would loop through classes which are on the class path. Finlaly, it will provide the needed configuration.

### What’s the problem Spring Framework solves?
Most important feature of Spring Framework is Dependency Injection. At the core of all Spring Modules is Dependency Injection or IOC Inversion of Control. When DI or IOC is used properly, we can develop loosely coupled applications. And loosely coupled applications can be easily unit tested.

### What else does Spring Framework solve?
* Remove duplicate/plumping codes
  - Reduce Boilerplate Code/ Reduce Duplication
  - Promote Decoupling/ Increase Unit Testablity
* Good Integration with Other Frameworks.
  - Hibernate for ORM
  - iBatis for Object Mapping
  - JUnit & Mockito for Unit Testing
  
### What is the core problem that Spring MVC Framework solves?
Spring MVC Framework provides decoupled way of developing web applications. With simple concepts like Dispatcher Servlet, ModelAndView and View Resolver, it makes it easy to develop web applications.

### Why do we need Spring Boot?
Spring based applications have a lot of configuration.
  * When we use Spring MVC, we need to configure component scan, dispatcher servlet, a view resolver, web jars(for delivering static content) among other things.
  * When we use Hibernate/JPA, we would need to configure a datasource, an entity manager factory, a transaction manager among a host of other things.

spring Boot looks at:
  - Frameworks available on the CLASSPATH 
  - Existing configuration for the application. 

Based on these, Spring Boot provides basic configuration needed to configure the application with these frameworks. This is called **Auto Configuration**.

Starters are a set of convenient dependency descriptors that you can include in your application. You get a one-stop-shop for all the Spring and related technology that you need, without having to hunt through sample code and copy paste loads of dependency descriptors. For example, if you want to get started using Spring and JPA for database access, just include the spring-boot-starter-data-jpa dependency in your project, and you are good to go.


### Dependency for Spring Boot Starter Web
Dependencies can be classified into:
* Spring - core, beans, context, aop
* Web MVC - (Spring MVC)
* Jackson - for JSON Binding
* Validation - Hibernate Validator, Validation API
* Embedded Servlet Container - Tomcat
* Logging - logback, slf4j

Any typical web application would use all these dependencies. Spring Boot Starter Web comes pre packaged with these. As a developer, I would not need to worry about either these dependencies or their compatible versions.

### Spring Boot Starter Project Options
As we see from Spring Boot Starter Web, starter projects help us in quickly getting started with developing specific types of applications.

* spring-boot-starter-web-services - SOAP (Single Object Access Protocol) Web Services
* spring-boot-starter-web - Web & RESTful applications
* spring-boot-starter-test - Unit testing and Integration Testing
* spring-boot-starter-jdbc - Traditional JDBC
* spring-boot-starter-hateoas - Add HATEOAS features to your services
* spring-boot-starter-security - Authentication and Authorization using Spring Security
* spring-boot-starter-data-jpa - Spring Data JPA with Hibernate (As the ORM framework)
* spring-boot-starter-cache - Enabling Spring Framework’s caching support
* spring-boot-starter-data-rest - Expose Simple REST Services using Spring Data REST

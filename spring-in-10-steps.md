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


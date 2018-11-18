# Java-Spring-notes
Some notes taken while studying Spring framework. This is not intended to be shared with others, so you might not understand what is going on. However, feel free to look at them.

## What is Spring framework?
Spring framework is a dependency injection framework

## Annotations
**@Component** annotation will tell Spring framework to create instances of the annotated class for you.
**@Autowired** annotation will tell String framework to search among the components to find the dependency for you.
**@Primary** To choose one between **dependency** components 

## Terminology
-   **Bean** is the different objects that are managed by Spring framework (the ones with @Component annotation).
-   **Autowiring** is the process where Spring identifies the dependence (the ones with @Autowired annotation), identifies the matches for the dependencies and populates them.
-   **Dependency injection**
-   **Inversion of control (IOC)** Classes that needs dependency was able to create an instance of the dependency. With Spring framework, the instantiation of dependency is handled by Spring framework. So, the control is inverted.
-   **IOC container** represents anything that is implementing IOC
-   **Application context** is the one where all the beans are created and managed. This is the important part of the spring framework. Here is where all the core logic of spring framework happens.

## How dependency works?
When we have @Autowired annotation on a variable, Spring framework looks for it and bring it. 
-	If the wired class was an **interface**, then, spring will find its implementation.
### What to do if there is a conflict?
-	If we have more than one implementation of an interface **and** have @Component on them:
	-	use **@Primary** annotation to use one of the dependencies. 
	-	put the name of the created instance as the name of one of the classed implements that interface.
``` InterfaceClass firstImplementdClass ```
	-	use **@Qualifier("firstImpl")**  in two places:
		-	In the class that implements the interface.
		-	Above the instantiation of the interface. Such as follows: 
```java
@Autowired
@Qualifier("firstImpl")
InterfaceClass interfaceInstance
```
**note:** If you are always using one implementation, it is better to use **@Primary**. However, if you are using different implementations interchangeably, use the name as the second point above.

## Scope of a bean
- **singleton** - One instance per Spring Context. 
	- **This is the default scenario**
	- If you have 4 application context => 4 singletons. Unlike GoF singleton where you have only one singleton per JVM.
- **prototype** - New bean whenever requested. use the following code above your class.
```java
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
```
use **SCOPE_SINGLETON** if you want only one instance. For singleton, you don't need to include the previous line because **singleton** is default. 
- **request** - One bean per HTTP request
- **session** - One bean per HTTP session
## How to make logs?
```java
private static Logger LOGGER = LoggerFactory.getLogger(SpringIn5StepsBasicApplication.class);
LOGGER.info("Hello there!");  
```
## Singleton vs Prototype
B is a dependancy of A. When creating 2 instances of A&B
```java
PersonDAO A= applicationContext.getBean(A.class);  
PersonDAO AA= applicationContext.getBean(A.class);  
  
LOGGER.info("{}", A);  
LOGGER.info("{}", A.getB());  
LOGGER.info("{}", AA);  
LOGGER.info("{}", AA.getB());
```
- A (singleton) B (singleton) => same adresses
- A (prototype) B (prototype) => different adresses
- A (prototype) B (singleton) => A different, B same
- A (singleton) B (prototype) =>  **same adresses**
	- this issue can be solved by adding proxy to the prototype such as follows:
```java
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE, proxyMode = ScopedProxyMode.TARGET_CLASS)
```
## External Componenets 
If you want to use componenets that are not in the same package, you need to use **@ComponenetScan(com.example.nasser)** annotation and provide it with the package.

## Life Cycle
Spring framework will make sure to destroy any component that is not being used. 
### What if I want to do something with the instance before destroying it?

### What if you want to do somethong after all dependecy have been populated?
Use **@PostConstruct** annotation with void method.
```java
@PostConstruct  
public void postConstruct(){}
```

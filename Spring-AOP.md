### Aspect-Oriendted Programming
Aspect-Oriented Programming (AOP) is a programming paradigm which complements Object-Oriented Programming (OOP)
by separating concerns of a software application to improve modularization. The separation of concerns (SoC)
aims for making a software easier to maintain by grouping features and behavior into manageable parts 
which all have a specific purpose and business to take care of.


**spring-aop** can intercept calls to beans and do somethings around that. 

**AspectJ** can do more, it can intercept change of values on a field.

### Cross-Cutting concerns
This means that the concerns are not for a specific layer. They are related to all layers. Examples of cross-cutting concerns:
* Logging
* Security 
* Performance
..etc

**AOP is the best approach for implementing cross-cutting concerns.**

### How to create an aspect?
* put **@Aspect** **@Configuration** annotation at the beginning of the aspect class.
* If you want to intercept before processing:
	+ Define **Aspect**, which is a combination of:
		- **Point-cut** what methods to intercept
		- **Advice** what to do with the intercepted call
		- **JoinPoin** specefic interception method
```java
//The execution(....) called Point-cut
@Before("execution(* com.example.spring.aop.springaop.business.*.*(..))")
public void before(JoinPoint joinPoint){
	//This area called (Advice)
        //What to do with the intercepted call
	// I want to log it
	logger.info("Intercepted method call - {}", joinPoint);
}
```
* Your main application should implements **CommandLineRunner**
```java
@SpringBootApplication
public class SpringAopApplication implements CommandLineRunner {

    Logger logger = LoggerFactory.getLogger(this.getClass());

    @Autowired
    Business1 business1;

    @Autowired
    Business2 business2;

	public static void main(String[] args) {
		SpringApplication.run(SpringAopApplication.class, args);
	}

    @Override
    public void run(String... args) throws Exception {
        logger.info(business1.calculateSomething());
        logger.info(business2.calculateSomething());
    }
}
```
* **Weaver** The framework which does the entire logic of making sure that the aspects is invoked at the right point.
* **Weaving** The process of doing that.

### After Aspet
```java
@Aspect
@Configuration
public class AfterAopAspect {
    Logger logger = LoggerFactory.getLogger(this.getClass());

    //What kind of methods I would intercept
    @AfterReturning(
            value = "execution(* com.example.spring.aop.springaop.business.*.*(..))",
            returning = "result")
	    public void afterReturning(JoinPoint joinPoint, Object result){
		logger.info("{} returned with value {}", joinPoint, result);
	    }
}
```

### Exception Aspect
It intercepts any thrown exceptions
```java
@AfterThrowing(
    value = "execution(* com.example.spring.aop.springaop.business.*.*(..))",
    throwing = "exception")
	public void afterThrowing(JoinPoint joinPoint, Object exception){
	logger.info("{} throw exception {}", joinPoint, exception);
}
```

### After Aspect
After exection interception
```java
@After(value = "execution(* com.example.spring.aop.springaop.business.*.*(..))")
public void after(JoinPoint joinPoint){
logger.info("after execution of {}", joinPoint);
}
```

### Around Aspect
To calculate the duration of execution

### Pointcuts best practices
* make a seperate class that hold all the pointcuts
```java
public class CommonJoinPointcutConfig {
    @Pointcut("execution(* com.example.spring.aop.springaop.data.*.*(..))")
    public void dataLayerExecution(){}
}
```
* Instead of 
```java
@Before("execution(* com.example.spring.aop.springaop.data.*.*(..))")
public void before(JoinPoint joinPoint){
logger.info("Allow execution for {}", joinPoint);
}
```
* Use the refrence
remember to put brakets in **dataLayerExecution()**
```java
@Before("com.example.spring.aop.springaop.aspect.CommonJoinPointcutConfig.dataLayerExecution()")
public void before(JoinPoint joinPoint){
logger.info("Allow execution for {}", joinPoint);
}
```
* You can do the samething for all layers togither.
```java
@Pointcut("com.example.spring.aop.springaop.aspect.CommonJoinPointcutConfig.businessLayerExecution()" +
            "&&" + "com.example.spring.aop.springaop.aspect.CommonJoinPointcutConfig.dataLayerExecution()")
public void allLayerExecution(){}
```
* If you want to intercept only beans, you can use:
```java
@Pointcut("bean(*dao*)")
public void beanContainingDao(){}
```
**Note** \*dao* is a regular expression

### Creating cusom annotation and Aspect 
* for time tracking of **methods** at **runtime**
Refer to this lesson 
https://www.udemy.com/spring-tutorial-for-beginners/learn/v4/t/lecture/7725838?start=0

### Aspect-Oriendted Programming
Aspect-Oriented Programming (AOP) is a programming paradigm which complements Object-Oriented Programming (OOP)
by separating concerns of a software application to improve modularization. The separation of concerns (SoC)
aims for making a software easier to maintain by grouping features and behavior into manageable parts 
which all have a specific purpose and business to take care of.


*spring-aop* can intercept calls to beans and do somethings around that. 
*AspectJ* can do more, it can intercept change of values on a field.

### Cross-Cutting concerns
This means that the concerns are not for a specific layer. They are related to all layers. Examples of cross-cutting concerns:
* Logging
* Security 
* Performance
..etc

*AOP is the best approach for implementing cross-cutting concerns.*

### How to create an aspect?
* put **@Aspect** **@Configuration** annotation at the beginning of the aspect class.
* If you want to intercept before processing:
```java
@Before("execution(* com.example.spring.aop.springaop.business.*.*(..))")
public void before(){
        //What to do with the intercepted call
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

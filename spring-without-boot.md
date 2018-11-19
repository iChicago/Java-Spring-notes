Remove
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
```

Add
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
</dependency>

<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
</dependency>

<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
</dependency>
```

In your main application:
* remove **@SpringBootApplication**
* add **@Configuration** => This is how spring do it using Java without spring-boot
* replace
```java
ApplicationContext applicationContext =
      SpringApplication.run(yourApplication.class, args);
```
* with
```java
ApplicationContext applicationContext =
      new AnnotationConfigApplicationContext(yourApplication.class);
```
* Spring boot was scanning for all required objects, now, we are not using spring-boot, so, we have to add it explicitly by using **@ComponentScan("com.example.nasser")**

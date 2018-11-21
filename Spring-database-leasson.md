### Using im memory database
* we added H2 as a dependancy in our ***pom.xml***
* now, we need to show the output of the database in our web consoule
  - in our ***application.properties***, add
```java
spring.h2.console.enabled=true
```
* to access the console, go to http://localhost:8080/h2-console/

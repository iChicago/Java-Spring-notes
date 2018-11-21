### Using im memory database
* we added H2 as a dependancy in our ***pom.xml***
* now, we need to show the output of the database in our web consoule
  - in our ***application.properties***, add
```java
spring.h2.console.enabled=true
```
* to access the console, go to http://localhost:8080/h2-console/


### JPA & Hibernate
Mapping a bean with a table in the database

* Defining an entity with Hibernate
```java
package com.example.spring.database.springdatabase.entities;


import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.Table;
import java.util.Date;

@Entity
@Table(name="person")
public class Person {

    @Id
    @GeneratedValue //to auto generate the IDs
    private int id;
    //if the name of the variable is different than the table name
    //then, use @column(name="name"). Anyway, here the names are matching
    private String name;
    private String location;
    //Java understands that birthDate is equal to the table birth_date
    private Date birthDate;

    public Person() {

    }

    //with Hibernate, we don't need to put the Id coulmn in the constructor
    public Person(int id, String name, String location, Date birthDate) {
        this.name = name;
        this.location = location;
        this.birthDate = birthDate;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getLocation() {
        return location;
    }

    public void setLocation(String location) {
        this.location = location;
    }

    public Date getBirthDate() {
        return birthDate;
    }

    public void setBirthDate(Date birthDate) {
        this.birthDate = birthDate;
    }

    @Override
    public String toString() {
        return "\n Person{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", location='" + location + '\'' +
                ", birthDate=" + birthDate +
                '}';
    }
}
```
### Creating a repository to manage the entity


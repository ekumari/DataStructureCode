### Spring Boot with JPA

Dependency

* spring-boot-starter-data-jpa
* @Entity - Entity which will be saved in the database
* @Id - primary key

application.properties

*   spring.jpa.show.sql = true
*   spring.h2.console.enable = true
*   data.sql - contains insert queries for data insertion

Connecting GET Rest API to JPA

```
@Repository - picked up by spring
public interface TodoJpaRepository extends JpaRepository<Todo, Long>{
    //Custom method
    List<Todo> findByUserName(String username); // exposes findByUserName, which you can call from service method.
}

But it has save() method for insert and so on.
```

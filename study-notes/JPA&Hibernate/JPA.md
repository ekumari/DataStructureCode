## Java Persistence API

Java is a OOP langauge. In Java, all data is stored in objects.
In Relational databases, store data in tables.

**Relational databases** are made up of Tables with concepts like normalization.

**But we need to establish a mapping between java object and relational database**

*   ORM - Object Relational Mapping
*   JPA provides mapping between your class and db tables.
    -  Using entities and relationship
    -  EntityManager: to save java objecto into db
    - JPQL: to search data from db

*   JPA provides annotations
    - @Id
    - @GeneratedValue
    - @Entity
    - @Table(name="Task")
    - @Column(name="description")
    - @ManyToMany - for relationship

    ```
    @Entity
    @Table(name="Task") - Task is table name
    public class Task{
        @Id
        @GeneratedValue
        private int id;

        @Column(name="description") - field in table
        private String desc;

        @Column(name="target_date")
        private Date targetDate;

        @Column(name="is_done")
        private boolean isDone;
    }
    ```
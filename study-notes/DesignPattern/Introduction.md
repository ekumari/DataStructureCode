## Design Pattern

*   It provides reusable solution for the common problems.

Types Of Design Pattern:

1. Crenational: About class instantiation or object creation.

    E.g: Factory Pattern, Abstract Factory Pattern, Singleton, Builder, Object Pool, Prototype.

    **UseCase1** : Developer wants to create DBConnection from different location, and he will create DB object at multiple locations which result in creating multiple connections from the database as each instance of DBConnection class will have a separate connection to the database.

    **Solution**: Create DBConnection class as a singleton class, so that only one instance of DBConnection is created and a single connection is established. Because we can manage DB Connection via one instance so we can control load balance, unnecessary connections, etc.

    **UseCase2**: Suppose you want to create multiple instances of similar kind and want to achieve loose coupling then you can go for **Factory pattern**. Consider an example of using multiple database servers like SQL Server and Oracle. If you are developing an application using SQL Server database as back end, but in future need to change database to oracle, you will need to modify all your code, so as factory design patterns maintain loose coupling and easy implementation we should go for factory for achieving loose coupling and creation of similar kind of object.s


2. Structural: 
3. Behavioural

## Autowiring

* Autowiring with XML
* @Autowired
* @Qualifier

```
public class Human{
    private Heart heart;

    public Human(Heart heart){
        this.heart = heart;
    }
    public void setHeart(Heart heart){
        this.heart = heart
    }
    public void startPumping(){
        if(heart != null){
            heart.pump();
        }else{
            print("You are dead");
        }
       
    }
}

public class Heart{
    public void pump(){
        print("heart is pumping");
    }


public class Body{
    public static void main(String args[]){
        ApplicationContext context = new ClassPathXMLApplicationContext("beans.xml");
        Human human = context.getBeans("human","Human.class");
        human.startPumping();
    }
}

<bean id="heartObject" class=com.coding.Heart></bean>

<bean id=human class=com.coding.Human>
<property name=heart ref=heartObject></property>
</bean>
```
### Hey, Spring could you automatically wire up my dependency ?

Yes
```
<bean id="heartObject" class=com.coding.Heart></bean>

<bean id=human class="com.coding.Human" autowire="byName">

</bean>
```
Autowire

    
* byType:  Create by type, spring check for type matched.
    ```
    <bean id="heartObject" class="com.coding.Heart></bean>
    <bean id=human class="com.coding.Human" autowire="byType"> check by Heart type
    ```
* byName: id name and ref variable name should be same
    * public Heart heart same bean id="heart"

* Constructor:  Define constructor and what to initialize
    ```
    public Human(Heart heart){
        this.heart = heart;
    }

    <bean id="heartObject" class="com.coding.Heart></bean>
    <bean id=human class="com.coding.Human" autowire="constructor"> check by Heart type
    ```
* default
* none

## @Autowired through annotation
```
@Autowired - Autowire by constructor
public Human(Heart heart){
    this.heart=heart
}

To make @Autowired on, then add 
<context:annotation-config /> in bean.xml

<bean id=human class="com.coding.Human"> Remove autowire from xml
```
## How @Autowired work?

    1. first it try to resolves with "byType"
    2. If byType fails then it goes with "byName"

@Qualifier Annotation

Autowiring is not possible for primitive or string type

why - How could spring know my data that i wanted to enter? e.g myRollNo, myName

```
<bean id="heartObject" class="com.coding.Heart></bean>
<bean id="humanHeart" class="com.coding.Heart></bean>

<bean id=human class="com.coding.Human"> 
```
Hey, spring here i have multiple implementation of heart class. So I need to use @Qualifier to tell what particular object needs to resolver.
```
@Autowired
@Qualifier("humanHeart") - resolver humanHeart
private Heart heart;
```
* @Autowired doesn't need a setter to do the dependency injection
* Using Qualifier to resolver the dependency
* Spring will create and inject your object to the matched dependency. No setter required.

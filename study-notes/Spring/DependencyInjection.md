### Dependency Injection

* Don't need to hard-coded the value
* Spring will inject all the dependency and initialize the value.
* Value get injected by spring.

## How spring inject the values?

* Setter injection
* Construction injection

### Spring Setter Injection
```
public class Student{
    private String studentName; //encapsulation property

    public void setName(String studentName){
        this.studentName = studentName;
    }
    public void display(){
        System.out.println("Student name is: "+studentName);
    }
}

public class Exam{
    public static void main(String agrs[]){
         ApplicationContext context = new ClassPathXMLApplicationContext("beans.xml");
         Student s = context.getBeans("student",Student.Class);

    }
}

<bean id="student" class="com.coding.Student">
    <property name="studentName" value="Anjani" /> - set the value
</bean>
```

### Spring Constructor Injection
```
public class Student{
    private String studentName; //encapsulation property
    private int id;

Here accepting as int. spring implicitly converts to int type
    Student(String studentName,int id){
        this.studentName = studentName;
        this.id = id;
    }
    public void display(){
        System.out.println("Student name is: "+studentName);
    }
}

public class Exam{
    public static void main(String agrs[]){
         ApplicationContext context = new ClassPathXMLApplicationContext("beans.xml");
         Student s = context.getBeans("student",Student.Class);

    }
}

<bean id="student" class="com.coding.Student">
    <constructor-arg name="studentName" value="Anjani" /> - set the value
    <constructor-arg name="id" value="1" /> value as string
     <constructor-arg name="id" value="1" type="int"/> explicitly provides int
</bean>
```
### Dependent Class
```
public class Student{
    String studentName;
    MathCheat mathCheat;
    //Setter for studentName and mathCheat
}

Student has dependency on MathCheat. But we will create one mathCheat and shared among all student.

<bean id="mathCheatObject" class="com.coding.MathCheat"></bean>
<bean id="student" class="com.coding.Student">
<property name="studentName" value="Anjani"></property>
<property name="mathCheat" ref="mathCheatObject">
</property>
</bean>

Refer to mathCheatObject, so to create single object of mathCheat.
```
Spring Important Feature:

* Spring IoC
* Dependency Injection
* Achieve loose coupling
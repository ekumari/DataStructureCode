## Interface

Like class, but the methods declared in an interface are abstract by default.
-   Interface is about what to do not how to do.
-   Total abstraction achieve
- interface can’t be instantiated
- A class can implement more than one interface.
- An interface can extends another interface or interfaces

-   If a class implement Abstract, and does not provide implementation for all the methods, then that class  must be declared as Abstract.
- E.g: Comparator Interface

interface <interface_name> {
    
    // declare constant fields
    // declare methods that abstract 
    // by default.
}

- Methods are public and abstract by default
- All fields are public, static and final by default.
- public : To make this method available for every implementation class.
  abstract : Implementation class is responsible to provide implementation.

### Why do we use interface ?

- To achieve total abstraction.
- Java does not support multiple inheritance so by using interface, it can support multiple inheritance.
- To achieve loose coupling.
- Interfaces are used to implement abstraction.

So question is why use interface when we have abstract classes?

Ans: Reason is Abstract class's variable is non final whereas in interface, variables are public, static and final.

Interface Usage: To put all the common functionalites and lets subclass implement  all these functionalities in their own class in their own way.

```
interface Vehicle { 
      
    // all are the abstract methods. 
    void changeGear(int a); 
    void speedUp(int a); 
    void applyBrakes(int a); 
} 
  
class Bicycle implements Vehicle{ 
      
    int speed; 
    int gear; 
      
     // to change gear 
    @Override
    public void changeGear(int newGear){ 
          
        gear = newGear; 
    } 
      
    // to increase speed 
    @Override
    public void speedUp(int increment){ 
          
        speed = speed + increment; 
    } 
      
    // to decrease speed 
    @Override
    public void applyBrakes(int decrement){ 
          
        speed = speed - decrement; 
    } 
      
    public void printStates() { 
         System.out.println("speed: " + speed 
              + " gear: " + gear); 
    } 
} 
  
class Bike implements Vehicle { 
      
    int speed; 
    int gear; 
      
    // to change gear 
    @Override
    public void changeGear(int newGear){ 
          
        gear = newGear; 
    } 
      
    // to increase speed 
    @Override
    public void speedUp(int increment){ 
          
        speed = speed + increment; 
    } 
      
    // to decrease speed 
    @Override
    public void applyBrakes(int decrement){ 
          
        speed = speed - decrement; 
    } 
      
    public void printStates() { 
         System.out.println("speed: " + speed 
             + " gear: " + gear); 
    } 
      
} 
class GFG { 
      
    public static void main (String[] args) { 
      
        // creating an inatance of Bicycle  
        // doing some operations  
        Bicycle bicycle = new Bicycle(); 
        bicycle.changeGear(2); 
        bicycle.speedUp(3); 
        bicycle.applyBrakes(1); 
          
        System.out.println("Bicycle present state :"); 
        bicycle.printStates(); 
          
        // creating instance of the bike. 
        Bike bike = new Bike(); 
        bike.changeGear(1); 
        bike.speedUp(4); 
        bike.applyBrakes(3); 
          
        System.out.println("Bike present state :"); 
        bike.printStates(); 
    } 
} 
```

### New features added in interface in JDK 8

-   Prior to JDK8, interface could not provide implementation. We can now add default implementation for interface methods.
-   Define static methods in interface which can be called independently without an object. Note: these method are not inherited.

### New features added in interfaces in JDK 9
From Java 9 onwards, interfaces can contain following also

    Static methods
    Private methods
    Private Static methods

### Access specifier of classes or interface

Access modifier:

1) private (accessible within the class where defined)
2) default or package private (when no access specifier is specified)
3) protected
4) public (accessible from any class)

But, the classes and interfaces themselves can have only two access specifiers when declared outside any other class.
1) public
2) default (when no access specifier is specified)

### Abstract Class

*   Abstract cannot be instantiated but we can have reference of abstract class.
* A Constructor of abstract class is called when an instance(or object) of inherited class is created
* A abstract class without any abstract method- Possible.
* Abstract class can have final methods.

Exercise:
1. Is it possible to create abstract and final class in Java?
2. Is it possible to have an abstract method in a final class?
3. Is it possible to inherit from multiple abstract classes in Java?

### Difference between Abstract Class and Interface in Java

Abstraction: Hiding the internal implementation and showing only functionality to the users.
E.g what it works (Showing) and How it works (Hiding)

1. Types of methods: Abstract class can have abstract or non-abstract method but interface can have only abstract method. From Java 8, it can have default and static.
2. Final Variables: Interface variables is final but Abstract may contain non-final variable.
3. Type of variables: Abstract class can have final, non-final, static and non-static variables. Interface has only static and final variables.
4. Implementation: Abstract class can provide the implementation of interface. Interface can’t provide the implementation of abstract class.
5. Accessibility of Data Members: Members of a Java interface are public by default. A Java abstract class can have class members like private, protected, etc.

### When to Use What?

**ABSTRACTION** 
-   Share common code
-   Non-static and non-final fields, you can access it
-   Provide access modifer other than public (Protected and private)

**INTERFACE**
-  Total abstraction.
-  Multiple Inheritance
-  Specify behaviour of particular data type, but not concerned with who implements its behaviour.

### Comparator Interface in Java with Examples
- It is used to order the List containing object of user-defined classes. <List only>
- Present in java.util package
- contains 2 method: compare(obj1,obj2) and equals(obj)

Q. Suppose we have an array/arraylist of our own class type say Student class, containing fields like rollno, name, address, DOB etc and we need to sort the array based on Roll no or name.

Ans: Using comparator interface, we can sort the array of user-defined based on data member.

```
class Sortbyroll implements Comparator<Student>  // Implements Comparator of user defined class type
{ 
    // Used for sorting in ascending order of 
    // roll number 
    public int compare(Student a, Student b) 
    { 
        return a.rollno - b.rollno; // -1(b is greater),0(equal),1 (a is greater)
    } 
} 

Collections.sort(ar, new Sortbyroll()); 
```
Compare by name and age:

```
static class CustomerSortingComparator implements Comparator<Student> { 
  
        @Override
        public int compare(Student customer1, Student customer2) { 
  
            // for comparison 
            int NameCompare = customer1.getName().compareTo(customer2.getName()); 
            int AgeCompare = customer1.getAge().compareTo(customer2.getAge()); 
  
            // 2-level comparison using if-else block 
            if (NameCompare == 0) { 
                return ((AgeCompare == 0) ? NameCompare : AgeCompare); 
            } else { 
                return NameCompare; 
            } 
        } 
    } 
```
### Nested Interface in a class

A interface inside a class can have public,protected and default not private.
className.interfaceName

### Nested Interface in a class

Inteface member can only be public. So interface inside another inside should be public.

### Nested Class in CLass

- Two types: static and inner class(Local and Annoymous class)
- Object of inner class is strongly associated with Outer class
- Object of static class is not strongly assiciated with outer class

Inner Class
1. 	Without an outer class object existing, there cannot be an inner class object. That is, the inner class object is always associated with the outer class object. 	
2. 	Inside normal/regular inner class, static members can’t be declared.
3. 	As main() method can’t be declared, regular inner class can’t be invoked directly from the command prompt.
4. 	Both static and non static members of outer class can be accessed directly. 

Static Class:
1. Without an outer class object existing, there may be a static nested class object. That is, static nested class object is not associated with the outer class object.	
2. Inside static nested class, static members can be declared.
3. As main() method can be declared, the static nested class can be invoked directly from the command prompt.
4. Only a static member of outer class can be accessed directly.


### Static method in Interface in Java

- Provides Default functionalities, cannot be overriden by subclass.
- Scope of the static method definition is within the interface only.

### Functional Interface

A functional interface contains only abstract method.
From Java 8, Lambda expression is used to represent the instance of a functional interface.
E.g: Runnable, Comparable, Comparator and ActionListener.
Before Java 8, we had to create anonymous inner class objects or implement these interfaces.

new Thread(new Runnable() 
        { 
            @Override
            public void run() 
            { 
                System.out.println("New thread created"); 
            } 
        }).start(); 

Java 8 onwards, we can assign lambda expression to its functional interface object like this:

// lambda expression to create the object 
    new Thread(()-> 
       {System.out.println("New thread created");}).start(); 

**@FunctionalInterface Annotation**s
@FunctionalInterface annotation is used to ensure that the functional interface can’t have more than one abstract method.

@FunctionalInterface
interface Square 
{ 
    int calculate(int x); 
} 

// lambda expression to define the calculate method 
        Square s = (int x)->x*x; 

**Important Points/Observations:**

-   A functional interface has only one abstract method but it can have multiple default methods.
-   @FunctionalInterface annotation is used to ensure an interface can’t have more than one abstract method. The use of this annotation is optional.
-   The java.util.function package contains many builtin functional interfaces in Java 8.

### Marker interface in Java

- Empty interface(no fields or methods).
- Example: Serializable, Clonnable and Remote Interface.

public interface Serializable 
{
  // nothing here
}

```
    A a = new A(20,"GeeksForGeeks"); 
    
        // Serializing 'a' 
        FileOutputStream fos = new FileOutputStream("xyz.txt"); 
        ObjectOutputStream oos = new ObjectOutputStream(fos); 
        oos.writeObject(a); 
  
        // De-serializing 'a' 
        FileInputStream fis = new FileInputStream("xyz.txt"); 
        ObjectInputStream ois = new ObjectInputStream(fis); 
        A b = (A)ois.readObject();//down-casting object 
```
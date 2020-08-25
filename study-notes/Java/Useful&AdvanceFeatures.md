## Generics

It allows Type(Integer, String, User-defined and etc) to be a parameter to methods, classes and interfaces.
E.g  HashSet, ArrayList, HashMap, etc use generics very well

// To create an instance of generic class 
BaseType <Type> obj = new BaseType <Type>()

Note: In Parameter type we can not use primitives like 
      'int','char' or 'double'.

Features:
- Used in writing Generics Class
- Used in writing Generics Functions
- Code Reuse: We can write a method/class/interface once and use for any type we want.
- Type Safety : Generics make errors to appear compile time than at run time.

```
// Creatinga an ArrayList without any type specified 
        ArrayList al = new ArrayList(); 
  
        al.add("Sachin"); 
        al.add("Rahul"); 
        al.add(10); // Compiler allows this 

At Run Time:
Exception in thread "main" java.lang.ClassCastException: 
   java.lang.Integer cannot be cast to java.lang.String
	at Test.main(Test.java:19)
```
Q. How generics solve this problem?

// Creating a an ArrayList with String specified 
        ArrayList <String> al = new ArrayList<String> ();  // String Specify beforehand, so compiler detect the error.
  
        al.add("Sachin"); 
        al.add("Rahul"); 
  
        // Now Compiler doesn't allow this 
        al.add(10);

- Individual Type casting is not needed.

// Creating a an ArrayList with String specified 
        ArrayList <String> al = new ArrayList<String> (); 
  
        al.add("Sachin"); 
        al.add("Rahul"); 
  
        // Typecasting is not needed  
        String s1 = al.get(0); 
        String s2 = al.get(1); 

- Implementing generic algorithms: By using generics, we can implement algorithms that work on different types of objects and at the same they are type safe too. 

## Assertions

Assertion allows testing the correctness of any assumptions that have been made in the program.
The assert statement is used with a Boolean expression and can be written in two different.

Syntax-
assert expression;
assert expression1 : expression2;

Example:
int value = 15; 
assert value >= 20 : " Underweight"; 

You need to enable assertions, by default it is disabled.
Enabling Assertions:
java –ea Test
java –enableassertions Test

Disabling Assertions:
java –da Test
java –disableassertions Test

## Annotations

Annotations are used to provide supplement information about a program.
Start with @

For more details: https://www.geeksforgeeks.org/annotations-in-java/

## Serializations and Deserializations

Serialization is a mechanism of converting the state of an object into a byte stream. 
Deserialization is the reverse process where the byte stream is used to recreate the actual Java object in memory.

![image info](..\images\serialize-deserialize-java.png
)

The byte stream created is platform independent. So, the object serialized on one platform can be deserialized on a different platform.

To make java object Serializable -> Implement Serializable interface
- ObjectOutputStream class contains writeObject() method for serializing an Object.
    public final void writeObject(Object obj) throws IOException

-  ObjectInputStream class contains readObject() method for deserializing an object.

    public final Object readObject() throws IOException, ClassNotFoundException

### Advanage of Serialization
    - Save/Persist state of an object.
    - Travel an object across a network.

![image info](..\images\serialization-5.jpg
)

**Serializable is a marker interface (has no data member and method). It is used to “mark” java classes so that objects of these classes may get certain capability. Other examples of marker interfaces are:- Cloneable and Remote.**

### Imp. Points to Remember: 
- If Parent class implement Serializable then child class doesn't need to implement but vice-versa is not true.
- Only non-static data member are saved via Serialization Process
- Static data members and transient data members are not saved via Serialization process

### SerializationUID

SerialVersionUID is used during Deserialization to verify that sender and reciever of a serialized object have loaded classes for that object which are compatible with respect to serialization.
If the reciever has loaded a class for the object that has different UID than that of corresponding sender’s class, the Deserialization will result in an **InvalidClassException**.

- Recommended that all serializable classes explicitly declare serialVersionUID value
- Use private modifier for UID since it is not useful as inherited member.

private static final long serialversionUID = 129348938L; 

Transient variables:- A variable defined with transient keyword is not serialized during serialization process.This variable will be initialized with default value during deserialization. (e.g: for objects it is null, for int it is 0).

Static Variables:- A variable defined with static keyword is not serialized during serialization process.This variable will be loaded with current value defined in the class during deserialization.

```
import java.io.*; 
  
class Emp implements Serializable { 
private static final long serialversionUID = 
                                 129348938L; 
    transient int a; 
    static int b; 
    String name; 
    int age; 
  
    // Default constructor 
public Emp(String name, int age, int a, int b) 
    { 
        this.name = name; 
        this.age = age; 
        this.a = a; 
        this.b = b; 
    } 
  
} 
  
public class SerialExample { 
public static void printdata(Emp object1) 
    { 
  
        System.out.println("name = " + object1.name); 
        System.out.println("age = " + object1.age); 
        System.out.println("a = " + object1.a); 
        System.out.println("b = " + object1.b); 
    } 
  
public static void main(String[] args) 
    { 
        Emp object = new Emp("ab", 20, 2, 1000); 
        String filename = "shubham.txt"; 
  
        // Serialization 
        try { 
  
            // Saving of object in a file 
            FileOutputStream file = new FileOutputStream 
                                           (filename); 
            ObjectOutputStream out = new ObjectOutputStream 
                                           (file); 
  
            // Method for serialization of object 
            out.writeObject(object); 
  
            out.close(); 
            file.close(); 
  
            System.out.println("Object has been serialized\n"
                              + "Data before Deserialization."); 
            printdata(object); 
  
            // value of static variable changed 
            object.b = 2000; 
        } 
  
        catch (IOException ex) { 
            System.out.println("IOException is caught"); 
        } 
  
        object = null; 
  
        // Deserialization 
        try { 
  
            // Reading the object from a file 
            FileInputStream file = new FileInputStream 
                                         (filename); 
            ObjectInputStream in = new ObjectInputStream 
                                         (file); 
  
            // Method for deserialization of object 
            object = (Emp)in.readObject(); 
  
            in.close(); 
            file.close(); 
            System.out.println("Object has been deserialized\n"
                                + "Data after Deserialization."); 
            printdata(object); 
  
            // System.out.println("z = " + object1.z); 
        } 
  
        catch (IOException ex) { 
            System.out.println("IOException is caught"); 
        } 
  
        catch (ClassNotFoundException ex) { 
            System.out.println("ClassNotFoundException" + 
                                " is caught"); 
        } 
    } 
} 

Output:

Object has been serialized
Data before Deserialization.
name = ab
age = 20
a = 2
b = 1000
Object has been deserialized
Data after Deserialization.
name = ab
age = 20
a = 0
b = 2000
```

## Lambda Expression

- Provides implementation of functional interface. Express instance of functional interface(Single Abstract Method only).

![image info](..\images\lambda-expression.jpg
)

Syntax:

 lambda operator -> body

FuncInter1 add = (int x, int y) -> x + y; 
FuncInter2 fobj = message ->System.out.println("Hello "+ message); 

### Important Points:

- Single statement then curly brackets is not needed
- More than one statements, then enclosed in curly brackets
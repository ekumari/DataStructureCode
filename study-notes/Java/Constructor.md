## Constructor

It is used to initialize values of the class at the time of object creation.

Rules of Constructor:
- Must have same name
- Cannot be abstract,final,static and synchronized.
- Can overload constructor 


Does constructor return any value?
-   There are no “return value” statements in constructor, but constructor returns current class instance. We can write ‘return’ inside a constructor.

### Default Constructor

-   Java automatically creates default constructor if there is no default or parameterized constructor written by user.
- default value numeric to 0, boolean to false and reference to null

### Assigning values to static final variables in Java

- static final variables cannot be assigned value in constructor; they must be assigned a value with their declaration or inside static block.
- Such behavior is obvious as static variables are shared among all the objects of a class; creating a new object would change the same static variable which is not allowed if the static variable is final.

### Copy Constructor in Java

// copy constructor 
    Complex(Complex c) { 
        System.out.println("Copy constructor called"); 
        re = c.re; 
        im = c.im; 
    } 

Complex c1 = new Complex(10, 15); 
          
// Following involves a copy constructor call 
Complex c2 = new Complex(c1);

### Private Constructors and Singleton Classes in Java

Q. Can we have private constructors ?
- Yes, only accessed inside the class.

Q. Do we need such ‘private constructors ‘ ?
- We need for singleton design pattern.

Q. What is a Singleton class?

- As the name implies, a class is said to be singleton if it limits the number of objects of that class to one. Singleton classes are employed extensively in concepts like Networking and Database Connectivity.

```
class MySingleton 
{ 
    static MySingleton instance = null; 
    public int x = 10; 
    
    // private constructor can't be accessed outside the class 
    private MySingleton() {  } 
   
    // Factory method to provide the users with instances 
    static public MySingleton getInstance() 
    { 
        if (instance == null)         
             instance = new MySingleton(); 
   
        return instance; 
    }  
} 
```
Q. Do we have destructors in Java?
- No, Java does garbage collection automatically.

### Important points to be taken care while doing Constructor Overloading :
- Constructor overloading is used when we have different ways of initializing the object.
- Constructor calling must be the first statement of constructor in Java.
- Recursive constructor calling is invalid in java.








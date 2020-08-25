## List of Important Keywords

Keyword is reserved word, it should not be used anywhere else, doing this it throws compile time error.

1.  **abstract**
    -   It is a non-access modifier for classes, methods but not for variables. 
    -   Used for abstraction

    *   Abstract Class: Partial implementation (Not all methods have definition). Due to their partial implementation, we cannot instantiate abstract classes.

    *   Any subclass of an abstract class must either implement all of the abstract methods in the super-class, or be declared abstract itself.

### Important rules for abstract methods:

- Any class which contains one or more abstract method(s), must declared abstract.
- Abstract class cannot be used to create objects, but they can be used to create object reference.

**Abstract & Final** :

They can be used together in a class or methods.
Class: Final is used to stop inheritence whereas Abstract class depends upon their subclasses for complete implementation. 
Methods: Final is used to prevent from overriding whereas abstract methods need to be overridden in sub classes.

2. **enum** : It is used to define enum in Java

3. **instanceof** : It is used to know whether the object is an instance of the specified type (class or subclass or interface).

4. **private** : It is an access modifier.Anything declared private cannot be seen outside of its class.

5. **protected** : Outside class, out side package only thruough inheritence.

6. **public** : Anything declared public can be accessed from anywhere.

7. **Synchronized**: For synchronization in java, means support multi-thread operations.

8. **this**: Refer to current class object

9. **super**: Refer to parent's class object

### Static Keyword

- This is non-access modifier. 
- Applicable for blocks, variables, methods, nested class
- When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object

Static Block:
```
// Java program to demonstrate use of static blocks 
class Test 
{ 
	// static variable 
	static int a = 10; 
	static int b; 
	
	// static block 
	static { 
		System.out.println("Static block initialized."); 
		b = a * 4; 
	} 

	public static void main(String[] args) 
	{ 
	System.out.println("from main"); 
	System.out.println("Value of a : "+a); 
	System.out.println("Value of b : "+b); 
	} 
} 

```
output
```
Static block initialized.
from main
Value of a : 10
Value of b : 40
```
**Static variables** : A single copy of variable get created and shared among all objects at class level.All instances of the class share the same static variable.

* static block and static variables are executed in order they are present in a program.

**Static Methods**: 
-   They can directly access other static data or methods.
```
// java program to demonstrate restriction on static methods 
class Test 
{ 
	// static variable 
	static int a = 10; 
	
	// instance variable 
	int b = 20; 
	
	// static method 
	static void m1() 
	{ 
		a = 20; 
		System.out.println("from m1"); 
		
		// Cannot make a static reference to the non-static field b 
		b = 10; // compilation error 
				
		// Cannot make a static reference to the 
				// non-static method m2() from the type Test 
		m2(); // compilation error 
		
		// Cannot use super in a static context 
		System.out.println(super.a); // compiler error 
	} 
	
	// instance method 
	void m2() 
	{	 
		System.out.println("from m2"); 
	} 
	
	
	
	public static void main(String[] args) 
	{ 
		// main method 
	} 
} 
```

When to use static variables and methods?
-  When some property is common to all the object of the class. E.g College name for all students.


### Final Keyword

![image info](..\images\final-keyword-in-java.jpg
)

- A black final variable can be initialized inside instance initializer block or inside constructor.If you have more than one constructor in your class then it must be initialized in all of them, otherwise compile time error will be thrown.

- A blank final static variable can be initialized inside static block.

**Reference final variable** - internal state of the object pointed by that reference variable can be changed. But not the reference as reference is final. This property of final is called non-transitivity
```
// Java program to demonstrate 
// reference final variable 

class Gfg 
{ 
	public static void main(String[] args) 
	{ 
		// a final reference variable sb 
		final StringBuilder sb = new StringBuilder("Geeks"); 
		
		System.out.println(sb); 
		
		// changing internal state of object 
		// reference by final reference variable sb 
		sb.append("ForGeeks"); 
		
		System.out.println(sb); 
	}	 
} 
```
```
Geeks
GeeksForGeeks
```
*   Final with for-Each is a legal statement.
for (final int i : arr) 
            System.out.print(i + " "); 
    }   

** Final with class to create immutable class.

### final, finally and finalize in Java?

final: we know from above
finally: Used in try catch block, guarantees that some piece of code will be executed, even if an exception is thrown.

```
// A Java program to demonstrate finally. 
class Geek { 
	// A method that throws an exception and has finally. 
	// This method will be called inside try-catch. 
	static void A() 
	{ 
		try { 
			System.out.println("inside A"); 
			throw new RuntimeException("demo"); 
		} 
		finally
		{ 
			System.out.println("A's finally"); 
		} 
	} 

	// This method also calls finally. This method 
	// will be called outside try-catch. 
	static void B() 
	{ 
		try { 
			System.out.println("inside B"); 
			return; 
		} 
		finally
		{ 
			System.out.println("B's finally"); 
		} 
	} 

	public static void main(String args[]) 
	{ 
		try { 
			A(); 
		} 
		catch (Exception e) { 
			System.out.println("Exception caught"); 
		} 
		B(); 
	} 
} 
```
Output:

```
inside A
A's finally
Exception caught
inside B
B's finally
```
* finally is meant to execute whether an exception occurs or not.
*   Application of finally block: So basically the use of finally block is resource deallocation. Means all the resources such as Network Connections, Database Connections, which we opened in try block are needed to be closed so that we won’t lose our resources as opened.

How jdk 1.7 makes usage of finally block as optional?
-   Until jdk 1.6 finally block is like a hero i.e, it is recommended to use it for resource deallocation but from jdk 1.7 onwards finally, block is now optional(however you can use it). Since the resources which we opened in the try block will automatically gets deallocated/closed when the flow of program reaches to the end of the try block.
This concept of automatic resource deallocation without using finally block is known as try-with-resources Statement.

Finalize Method:
It is a method that the Garbage Collector always calls just before the deletion/destroying the object which is eligible for Garbage Collection, so as to perform clean-up activity
Clean-up activity means closing the resources associated with that object like Database Connection, Network Connection or we can say resource de-allocation

Syntax: protected void finalize throws Throwable{}

- Object class contains the finalize method.
- Garbage Collector calls finalize method on that class object which is eligible for Garbage collection. So if String object is eligible for Garbage Collection then String class finalize method is going to be called.
- JVM does not ignore all exceptions while executing finalize method, but it ignores only Unchecked exceptions. If the corresponding catch block is there then JVM won’t ignore and corresponding catch block will be executed.
- System.gc() is just a request to JVM to execute the Garbage Collector. It’s up-to JVM to call Garbage Collector or not.Usually JVM calls Garbage Collector when there is not enough space available in the Heap area or when the memory is low.

### Transient keyword
transient is a variables modifier used in serialization. At the time of serialization, if we don’t want to save value of a particular variable in a file, then we use transient keyword. When JVM comes across transient keyword, it ignores original value of the variable and save default value of that variable data type.
transient and static works fine
transient and final works fine

```
class Test implements Serializable 
{ 
    // Making password transient for security 
    private transient String password; 
  
    // Making age transient as age is auto- 
    // computable from DOB and current date. 
    transient int age; 
  
    // serialize other fields 
    private String username, email; 
    Date dob; 
  
    // other code 
} 
```


### Volatile Keyword
-   Volatile is yet another way to make class thread safe.
volatile vs synchronized:
Mutual Exclusion: It means that only one thread or process can execute a block of code (critical section) at a time.
Visibility: It means that changes made by one thread to shared data are visible to other threads

*   Java’s synchronized keyword guarantees both mutual exclusion and visibility. If we make the blocks of threads that modifies the value of shared variable synchronized only one thread can enter the block and changes made by it will be reflected in the main memory. All other thread trying to enter the block at the same time will be blocked and put to sleep.

In some cases we may only desire the visibility and not atomicity. Use of synchronized in such situation is an overkill and may cause scalability problems. Here volatile comes to the rescue.

Volatile variables have the visibility features of synchronized but not the atomicity features. The values of volatile variable will never be cached and all writes and reads will be done to and from the main memory. However, use of volatile is limited to very restricted set of cases as most of the times atomicity is desired.
For example a simple increment statement such as x = x + 1; or x++ seems to be a single operation but is s really a compound read-modify-write sequence of operations that must execute atomically

### Strictfp Keyword
strictfp is a keyword in java used for restricting floating-point calculations and ensuring same result on every platform while performing operations in the floating-point variable.
Floating point calculations are platform dependent i.e. different output(floating-point values) is achieved when a class file is run on different platforms(16/32/64 bit processors). To solve this types of issue, strictfp keyword was introduced in JDK 1.2 version by following IEEE 754 standards for floating-point calculations. 

Important points: 
-   strictfp modifier is used with classes, interfaces and methods only
-   When a class or an interface is declared with strictfp modifier, then all methods declared in the class/interface, and all nested types declared in the class, are implicitly strictfp.
-   strictfp cannot be used with abstract methods. However, it can be used with abstract classes/interfaces
-   Since methods of an interface are implicitly abstract, strictfp cannot be used with any method inside an interface. 
strictfp interface Test 
{
    double sum();
    strictfp double mul(); // compile-time error here
}
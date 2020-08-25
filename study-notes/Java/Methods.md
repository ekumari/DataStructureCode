## Methods

It is stored in stack area. When the execution is completed, the allocated stack frame would be deleted.

### Return Type

-   We can return array of same type from method.
-   We can use Pair if there are only two returned values.
-   If more than 2 values, then return custom object which contains all the data.

### Overloading

It allows different methods to have same name but different signature.
It is compile time polymorphism.

Can we overload methods on return type?
-   We cannot overload by return type.  

Can we overload static methods?
-   Yes

Can we overload methods that differ only by static keyword?
- Not possible in a class

Can we Override static methods in java?
- Yes but then Base class method hides sub class method means when the call made to that method, then it will base class method over derived class method.

### Difference between Overloading and Overriding 

![image info](..\images\OverridingVsOverloading.png)

*   Overloading is an example of compiler time polymorphism and overriding is an example of run time polymorphism.

### Method overloading and null error in Java

```
public class Test 
{ 
    // Overloaded methods 
    public void fun(Integer i) 
    { 
        System.out.println("fun(Integer ) "); 
    } 
    public void fun(String name) 
    { 
        System.out.println("fun(String ) "); 
    } 
  
    // Driver code  
    public static void main(String [] args) 
    { 
        Test mv = new Test(); 
  
        // This line causes error 
        mv.fun(null); 
    } 
} 
```
Compile time error, Intger and String are not primitive data type, They boths accepts null values. So compile got confused which fun method to call.

To avoid the null error, pass the type as well

        Test mv = new Test(); 
          
        Integer arg = null; 
  
        // No compiler error 
        mv.fun(arg); 

### Overriding equals method in Java
```
    Complex c1 = new Complex(10, 15); 
        Complex c2 = new Complex(10, 15); 
        if (c1 == c2) { 
            System.out.println("Equal "); 
        } else { 
            System.out.println("Not Equal "); 
        } 
```
Not Equal as == refer to object reference. As they are different object having difference references.

**To point same reference:** 

Complex c3 = c1;  // (c3 == c1) will be true 


How do we check for equality of values inside the objects?

-   Object class has some basic methods, e.g clone(), toString() hashCode() and equals()

-   We can override the equals method in our class to check whether two objects have same data or not. 

Equals method override in subclass

public boolean equals(Object o) { 
  
        // If the object is compared with itself then return true   
        if (o == this) { 
            return true; 
        } 
  
        /* Check if o is an instance of Complex or not 
          "null instanceof [type]" also returns false */
        if (!(o instanceof Complex)) { 
            return false; 
        } 
          
        // typecast o to Complex so that we can compare data members  
        Complex c = (Complex) o; 
          
        // Compare the data members and return accordingly  
        return Double.compare(re, c.re) == 0
                && Double.compare(im, c.im) == 0; 
    } 

**Note** As a side note, when we override equals(), it is recommended to also override the hashCode() method. If we don’t do so, equal objects may get different hash-values; and hash based collections, including HashMap, HashSet, and Hashtable do not work properly (see this for more details).


Override toString method()-

```
//constructor
public Complex(double re, double im) { 
        this.re = re; 
        this.im = im; 
    } 

@Override
    public String toString() { 
        return String.format(re + " + i" + im); 
    } 

//From main
public static void main(String[] args) { 
        Complex c1 = new Complex(10, 15); 
        System.out.println(c1); 
    } 

```
Output: 10.0 + i15.0


In general, it is a good idea to override toString() as we get get proper output when an object is used in print() or println().

### Private and final methods in Java

Final method means we can't override this method. Private makes inaccessible. So it does not make sense to use both in the method.


**Java is strictly pass by value**

### Object CLonning In Java

**Shallow Copy**

```
Class A{
    int i;
    int j;
}

A obj = new A();
obj.i = 5;
obj.j = 6;

A obj1 = obj;
i=5 and j = 6
```

Here we are not creating  2 objects. its just the 2 reference pointing to same reference. So it is shallow copy. Any change to obj1 will reflect obj.

In heap, there is only one object obj. 
In stack, there are 2 references. obj and obj1

**Deep Copy**

Here, you will have 2  object and 2 reference.
```
A obj = new A();
obj.i = 5;
obj.j = 6;

A obj1 = new A();
obj1.i = obj.i;
obj1.j = obj.j;
```

But that's not the proper way. So, we used clone method of object.

A obj1 = obj.clone(); // Create object and contain the same value.

**Note** By default, you are not allow to clone object, for that you have give permission that is possible through implement interface.

Practical Knowledge: https://www.youtube.com/watch?v=WIh-TVq4ifI









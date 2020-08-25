## Array

- In Java all arrays are dynamically allocated.
- Clonning of Array: 
```
int intArray[] = {1,2,3}; 
int cloneArray[] = intArray.clone(); //Shallow Copy
Arrays.deepToString(intArray); // Deep Copy
```
- Default value
    int: 0
    String: null
    boolean: false
    Object: null

- Methods:
    equals Arrays.equals(intArr, intArr1)); 
    fills Arrays.equals(intArr, intArr1)); 
    hashCode Arrays.hashCode(intArr);
    sort Arrays.sort(intArr, 1, 3);
    comparator
    spliterator(originalArray, fromIndex, endIndex):  Arrays.spliterator(intArr, 1, 3)
    toString: String representation of Array content
    Arrays.deepEquals() which does deep comparison.

### util.Arrays vs reflect.Array in Java with Examples

Class Hierarchy of Array:

java.lang.Object
 ↳ java.lang.reflect
  ↳ Class Array

Class Hierarchy of Arrays:

java.lang.Object
 ↳ java.util
  ↳ Class Arrays

**Immutability**:
The Array class is immutable in nature whereas the Arrays class is not. By immutable, it means that the class cannot be extended or inherited. The Array class is declared as final to achieve immutability.

Class Declaration of Array:

public final class Array
    extends Object

Class Declaration of Arrays:

public class Arrays
    extends Object

**Usage**:
The java.util.Arrays class contains various methods for manipulating arrays (such as sorting and searching) whereas this java.lang.reflect.Array class provides static methods to dynamically create and access Java arrays. This Array class keeps the array to be type-safe.

### Final Array

So a final array means that the array variable which is actually a reference to an object, cannot be changed to refer to anything else, but the members of array can be modified.

```
class Test  
{ 
    int p = 20; 
    public static void main(String args[]) 
    { 
       final Test t = new Test();        
       t.p = 30; 
       System.out.println(t.p);    print 30, variable value can be changed 
    }     
} 
```

```
class Test  
{ 
    int p = 20; 
    public static void main(String args[]) 
    { 
       final Test t1 = new Test();        
       Test t2 = new Test(); 
       t1 = t2;  
       System.out.println(t1.p);       // compile error: cannot assign value to final variable t1
    }     
} 
```

```
Predict the output
class Test  
{ 
    public static void main(String args[]) 
    { 
       final int arr1[] = {1, 2, 3, 4, 5}; 
       int arr2[] = {10, 20, 30, 40, 50}; 
       arr2 = arr1;       
       arr1 = arr2;   
       for (int i = 0; i < arr2.length; i++) 
          System.out.println(arr2[i]);   //work without error         
    }     
} 
```

### ArrayIndexOutOfBound Error

If a request for a negative or an index greater than or equal to size of array is made, then the JAVA throws a ArrayIndexOutOfBounds Exception.
The ArrayIndexOutOfBoundsException is a Runtime Exception thrown only at runtime.

### Array vs ArrayList in Java

Array:
- fixed size arrays
- can have primitive or objects
- functions are not supported

ArrayList:
- Dynamic size arrays
- supports object
- supports many additional methods such indexOf(), remove()

### ArrayList to Array Conversion in Java : toArray() Methods

- using toArray: list.toArray();
**Note**: toArray() method returns an array of type Object(Object[]). We need to typecast it to Integer before using as Integer objects. If we do not typecast, we get compilation error

### Merge arrays into a new object array in Java

In java8, stream API provide a way to do it.
java.lang.Object
  ↳  java.util.stream


Input : a[] = {1, 2, 3}
        b[] = {4, 5, 6}
Output : {1, 2, 3, 4, 5, 6}

  Stream.of(a, b).flatMap(Stream::of).toArray(); 

  - flatMap: flatten the stream which contains stream of element.
  - toArray: convert to array

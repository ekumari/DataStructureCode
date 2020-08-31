## Collection

### AbstractCollection Class
Abstract Class implements collection interface.

Methods:
-   add(E e)
-   addAll(Collection c)
-   clear()
-   contains(Object o): return true if collection contains the specified element.
-   containsALL(Collection c): return true if collection contains all the elements of specified collections
-   isEmpty()
- iterator()
-   remove(Object o)
-   size()
-   toArray(): return an array
-   toArray(T[] a): return an array and runtype of the returned array is that of the specified array. 

### Iterators

It is used in collection framework to retrieve element one by one.

#### Three iterators:

**Enumeration:**
-   To traverse legacy collections (Vector, Hashtable)

Use: Enumeration e = v.elements();

Methods: hasMoreElements(), nextElement()

```
Vector v = new Vector(); 
Enumeration e = v.elements();
while (e.hasMoreElements()) 
        { 
            // moving cursor to next element 
            int i = (Integer)e.nextElement(); 
  
            System.out.print(i + " "); 
        } 
```
Limitation:
-   Not universal iterator bcs it is a legacy iterator
-   Remove operation can't be performed.
-   Only forward directions iterations is possible.

**Iterator:**

It is a universal iterator as we can apply to any collection object.
Perform Read and Remove operations.

Use: Iterator itr = c.iterator(); // c is collection object

Methods: hasNext(), next(), remove()

**remove()** method can throw exceptions:
* UnsupportedOperationException: Remove operation is not supported
* IILegalStateException: Remove method has been called without next method.

```
ArrayList<Integer> al = new ArrayList<Integer>(); 
for (int i = 0; i < 10; i++) 
            al.add(i); 
  
System.out.println(al); 
  Iterator itr = al.iterator(); 
  
        // checking the next element availabilty 
        while (itr.hasNext()) 
        { 
            //  moving cursor to next element 
            int i = (Integer)itr.next(); 
  
            // getting even elements one by one 
            System.out.print(i + " "); 
  
            // Removing odd elements 
            if (i % 2 != 0) 
               itr.remove();  
        } 
        System.out.println();  
        System.out.println(al); 

Output:

[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
0 1 2 3 4 5 6 7 8 9 
[0, 2, 4, 6, 8]

```
Limitations:
-   Only forward direction iterating is possible.
-   Replacement and addition of new element is not supported by iterator.

**List Iterator:**

It is for List Collections (Arraylist, Linkedlist etc)
It provides bidirectional iteration. Forward and backward.
It extends iterator interface.

Use: ListIterator ltr = l.listIterator(); // l is any List object

Methods: hasNext(), next(), nextIndex(), hasPrevious(), previous(), previousIndex(), remove(), set(obj), add(obj)

set() method can throw four exceptions

    UnsupportedOperationException – if the set operation is not supported by this list iterator
    ClassCastException : If the class of the specified element prevents it from being added to this list
    IllegalArgumentException : If some aspect of the specified element prevents it from being added to this list
    IllegalStateException : If neither next nor previous have been called, or remove or add have been called after the last call to next or previous

add() method can throw three exceptions

    UnsupportedOperationException : If the add method is not supported by this list iterator
    ClassCastException : If the class of the specified element prevents it from being added to this list
    IllegalArgumentException : If some aspect of this element prevents it from being added to this list


```
ListIterator ltr = al.listIterator(); 
  
        // checking the next element availabilty 
        while (ltr.hasNext()) 
        { 
            //  moving cursor to next element 
            int i = (Integer)ltr.next(); 
  
            // getting even elements one by one 
            System.out.print(i + " "); 
  
            // Changing even numbers to odd and 
            // adding modified number again in  
            // iterator 
            if (i%2==0) 
            { 
                i++;  // Change to odd 
                ltr.set(i);  // set method to change value 
                ltr.add(i);  // to add 
            } 
        } 

O/P:

[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
0 1 2 3 4 5 6 7 8 9 
[1, 1, 1, 3, 3, 3, 5, 5, 5, 7, 7, 7, 9, 9, 9]

```

### Iterator vs Foreach In Java

Iterator: To traverse collection, We can modify collection by remove method

for (Iterator i = c.iterator(); i.hasNext(); ) 
       System.out.println(i.next());

For each: We can't modify collections. Throw ConcurrentModificationExceptions

 for (Element e: c)
       System.out.println(e);

Lambda Expression (Java 8)

elements.forEach (e -> System.out.println(e) );

**Iterator and for-each loop are faster than simple for loop for collections with no random access, while in collections which allows random access there is no performance change with for-each loop/for loop/iterator**


### Double Brace Initialization in Java

One ways: 
 Set<String> sets = new HashSet<String>(); 
        sets.add("one"); 
        sets.add("two"); 
        sets.add("three"); 
  // Now pass above collection as parameter to method 
        useInSomeMethod(sets); 

Second Way: Create an annonymous inner class.These inner classes are capable of accessing the behavior of their parent class

    Set<String> sets = new HashSet<String>() 
        { 
            { 
                add("one"); 
                add("two"); 
                add("three"); 
            } 
        }; 
  
        // ... 
  
        // Now pass above collection as parameter to method 
        useInSomeMethod(sets); 

### AbstractList

It implements Collection interface and AbstractCollection class.
java.lang.Object
 ↳ java.util.AbstractCollection<E>
    ↳ Class AbstractList<E>

**Methods**
Adding Elements:
-   add(E e)
-   add(int inxex, E element)
-   addAll(int inxex, Collection c)

-   clear()
-   equals(Object o)
-   get(int index)
-   hashCode()
-   indexOf(Object o)
-   iterator()
-   lastIndexOf(Object o)
-   listIterator()
-   listIterator(int index): list iterator over the elements in the list,starting at the specified position in the list.

Removing Elements
-   remove(object)
-   remove(int index)
-   removeRange(int fromIndex, int toIndex)

Changing Element
-   set(int index, E element)
-   subList(int fromIndex, int toIndex)

#### ArrayList

Found in java.util package

![image info](..\images\ArrayList.png
)

Methods: Same as AbstractList

**Important Features**

1. ArrayList inherits from AbstractList class and implements List interface.
2. Random access possible
3. Can't be used for primitive types like int, char, etc.Need a wrapper class.
4. ArrayList is not synchronized.Vector is Synchronized.

#### How ArrayList work internally?

Since ArrayList is a dynamic array and we do not have to specify the size while creating it, the size of the array automatically increases when we dynamically add and remove items. Though the actual library implementation may be more complex, the following is a very basic idea explaining the working of the array when the array becomes full and if we try to add an item:

    Creates a bigger sized memory on heap memory (for example memory of double size).
    Copies the current memory elements to the new memory.
    New item is added now as there is bigger memory available now.
    Delete the old memory.

#### Constructors in the ArrayList

1. ArrayList():
ArrayList arr = new ArrayList(); 

2. ArrayList(Collection c):
ArrayList arr = new ArrayList(c); 

3. ArrayList(int capacity):
ArrayList arr = new ArrayList(N); 

### LinkedList in Java

- Present in java.util package.
- Implementation of LinkedList data structure which is a linear data structure where the elements are not stored in contigous locations and every element is a separate object with data part and address part.
- Bcoz of dynamicity and ease of insertions and deletions, they are preferred over the arrays.
- Search operation is costly as  we need to traverse entire list.

Methods: Same as Abstract List plus some more methods 
    - addFirst(E e), addLast(E e), getFirst(), getLast()
    - offer(E e): Add the element at the last of list.
    - offerFirst(E e), offerLast(E e)
    - peek():Retrieves head of the element but doesn't remove, peekFirst(), peekLast()
    - poll():Retrieves and removes the head of this list. pollFirst(),pollLast()
    - removeLast(), removeFirst()

#### How LinkedList work Internally?

Since a LinkedList acts as a dynamic array and we do not have to specify the size while creating it, the size of the list automatically increases when we dynamically add and remove items. And also, the elements are not stored in a continuous fashion. Therefore, there is no need to increase the size. Internally, the LinkedList is implemented using the **doubly linked list data structure**. The main difference between a normal linked list and a doubly LinkedList is that a doubly linked list contains an extra pointer, typically called the previous pointer, together with the next pointer and data which are there in the singly linked list. 

#### Constructor:

1. LinkedList():
    LinkedList ll = new LinkedList(); 
2. LinkedList(Collection C):
    LinkedList ll = new LinkedList(C); 


### CopyOnWriteArrayList

* Introduced in JDK 1.5, implements List interface.
* Advanced version of ArrayList
* All modification( add, set, remove etc) are implemented by making fresh copy.
* Found in java.util.concurrent package

#### Difference between Synchronized ArrayList and CopyOnWriteArrayList

ArrayList
-   Not synchrozied
-   Synchronization of ArrayList:
    - Collections.synchronizedList()
    - CopyOnWriteArrayList

**Why CopyOnWriteArrayList came into existence when Collection.synchronizedList() was already present**

Initially, SynchronizedList was used in multithreaded environment but it had some limitations. All of its read and write methods were synchronized on the list object itself, i.e. if a thread is executing add() method, it blocks other threads which want to get the iterator to access elements in the list. Also, only one thread was allowed iterate the list’s elements at a time, which was inefficient. That was quite rigid.

Thus a more flexible collection was required which allows:

   - Multiple threads executing read operations concurrently.
   - One thread executing read operation and another executing write operation concurrently.
   - Only one thread can execute write operation while other threads can execute read operations simultaneously.

To overcome these issues, finally in Java 5, the new set of collection classes called Concurrent Collections was introduced which had CopyOnWriteArrayList in it.


When to use SynchronizedList?

    - Since in CopyOnWriteArrayList for every update/modify operations, a new separate cloned copy is created and there is overhead on JVM to allocate memory & merging cloned copy with original copy. Thus, in this case SynchronizedList is better option.
    - When size of Arraylist is large.


When to use CopyOnWriteArrayList?

    - The CopyOnWriteArrayList provides reading without a lock, which means a much better performance if there are more reader threads and write is happening quite low.
    - When the size of Arraylist is small.

SynchronizedList v/s CopyOnWriteArrayList

| SynchronizedList      | CopyOnWriteArrayList |
| ----------- | ----------- |
|   Locks the whole list during both read or write operation    | Locks the list during write operation only, so no lock during read operation, multiple threads excuting read operation concurrently       |
| Fail-fast iterator   | fail-safe iterator        |
| Java 1.2 | Java 1.5 |
| Iterations should be inside synchronized block | Safely iterate outside synchronized block |
| Throw ConcurrentModificationException | Doesn't allow modifying the list while traversing,will not throw ConcurrentModificationException |
| Best when ArrayList is large and write operation > read operation |Best when ArrayList is small or read operation > write operation | 

## Queue
- Queue interface present in java.util package, enxtends Collections interface.
- FIFO: First In First Out

![image info](..\images\Queue-Deque-in-Java-Collections.png
)

- PriorityQueue (Not thread safe) Class extends Abstract Queue implements Queue extends Collections
- LinkedList (Not thread safe) Class implements Deque extends Collections



### Create Queue
    Queue<Obj> queue = new PriorityQueue<Obj> (); 
    Queue<Integer> q = new LinkedList<>(); 

    - Add: q.add(8);
    - Remove head: q.remove();
    - Peek head: q.peek()
    - Size of Queue: q.size();

###  PriorityBlockingQueue
**PriorityBlockingQueue is one alternative implementation if thread safe implementation is needed**
- PriorityBlockingQueue is an unbounded blocking queue that uses the same ordering rules as class PriorityQueue and supplies blocking retrieval operations. 
- Unbounded: Resouce exhaust resulting in OutOfMemoryError

```
Queue<Integer> pbq = new PriorityBlockingQueue<Integer>(); 

        // Adding items to the pbq 
        // using add() 
        pbq.add(10); 
        pbq.add(20); 
        pbq.add(15); 

        pbq.peek(): 10
        pbq.poll(): 10
        pbq.peek(): 15
```
AbstractQueue: It provides skeletal implementations of some Queue operations.

Constructors in Java AbstractQueue:

    protected AbstractQueue(): The default constructor, but being protected, it doesn’t allow to create an AbstractQueue object.

### ArrayBlockingQueue 
- FIFO, but bounded as it uses Array so size is fixed.
- Syntax:
public class ArrayBlockingQueue
    extends AbstractQueue
        implements BlockingQueue, Serializable
- Constructor:
    ArrayBlockingQueue(int capacity)

### LinkedBlockingQueue

- LinkedBlockingQueue is an optionally-bounded blocking queue based on linked nodes.
- It means that the LinkedBlockingQueue can be bounded, if its capacity is given, else the LinkedBlockingQueue will be unbounded. 
- It means that the LinkedBlockingQueue can be bounded, if its capacity is given, else the LinkedBlockingQueue will be unbounded. 
- FIFO

Constructor Summary:
    - LinkedBlockingQueue()
    - LinkedBlockingQueue(Collection c)
    - LinkedBlockingQueue(int initialCapacity)

## Deque interface

- Present in java.util
- Double-Ended Queue that supports addition or removal of elements from either end of data structure.
- It can either be used as a queue(first-in-first-out/FIFO) or as a stack(last-in-first-out/LIFO)

## SET
- set interface present in the java.util package and extends the Collection interface
- Unordered Collection( Doesnt retain insertion order), No Duplicates

![image info](..\images\Set-TreeSet-SortedSet-In-Java-Collection.png
)

### Syntax:

Set<String> hash_Set = new HashSet<String>();
hash_Set.add("Geeks"); 
        hash_Set.add("For"); 
        hash_Set.add("Geeks"); 
        hash_Set.add("Example"); 
        hash_Set.add("Set"); 

[Set, Example, Geeks, For]

Set provides method for mathematical Union, Intersection and difference.

Set<Integer> a = new HashSet<Integer>();  
a.addAll(Arrays.asList(new Integer[] {1, 3, 2, 4, 8, 9, 0}));  
Set<Integer> b = new HashSet<Integer>();  
b.addAll(Arrays.asList(new Integer[] {1, 3, 7, 5, 4, 0, 7, 5}));  

// To find union  
        Set<Integer> union = new HashSet<Integer>(a);  
        union.addAll(b); 

// To find intersection  
        Set<Integer> intersection = new HashSet<Integer>(a);  
        intersection.retainAll(b);

// To find the symmetric difference  
        Set<Integer> difference = new HashSet<Integer>(a);  
        difference.removeAll(b);

Union of the two Set[0, 1, 2, 3, 4, 5, 7, 8, 9]
Intersection of the two Set[0, 1, 3, 4]
Difference of the two Set[2, 8, 9]

### HASHSET

- Implements SET interface, backed by hash table which is internally a hashMap instance.
- No order
- Permits null element
- Constant time for ADD, REMOVE, CONTAINS and SIZE assuming the hash function disperses the elements properly among the buckets.
- Underlying data structure is HashTable
- No Duplicates
- HashSet also implements Searlizable and Cloneable interfaces

NOTE: The implementation in a HashSet is not synchronized
Set s = Collections.synchronizedSet(new HashSet(...));

Constructors in HashSet:

    HashSet h = new HashSet();
    Default initial capacity is 16 and default load factor is 0.75.
    HashSet h = new HashSet(int initialCapacity);
    default loadFactor of 0.75
    HashSet h = new HashSet(int initialCapacity, float loadFactor);
    HashSet h = new HashSet(Collection C);

```

// Java program to demonstrate working of HashSet 
import java.util.*; 

class Test 
{ 
	public static void main(String[]args) 
	{ 
		HashSet<String> h = new HashSet<String>(); 

		// Adding elements into HashSet usind add() 
		h.add("India"); 
		h.add("Australia"); 
		h.add("South Africa"); 
		h.add("India");// adding duplicate elements 

		// Displaying the HashSet 
		System.out.println(h); 
		System.out.println("List contains India or not:" + 
						h.contains("India")); 

		// Removing items from HashSet using remove() 
		h.remove("Australia"); 
		System.out.println("List after removing Australia:"+h); 

		// Iterating over hash set items 
		System.out.println("Iterating over list:"); 
		Iterator<String> i = h.iterator(); 
		while (i.hasNext()) 
			System.out.println(i.next()); 
	} 
} 

[South Africa, Australia, India]
List contains India or not:true
List after removing Australia:[South Africa, India]
Iterating over list:
South Africa
India
```
Internal working of a HashSet:

All the classes of Set interface internally backed up by Map. HashSet uses HashMap for storing its object internally. 

Key contains Set Elements
Value will be "PRESENT"

public boolean add(E e)
{
   return map.put(e, PRESENT) == null;
}

**Time Complexity of HashSet Operations:**

HashSet takes O(1) time

Methods:
- add(E e)
- clear()
- contains(Object o)
- remove(Object o)
- iterator()
- isEmpty()
- size()
- clone()

### TreeSet

- Implementation of SortedSet interface
- Sorted order
- Accepts Homogeneous type, Hetrogenous return classCastException

```
// Java program to demonstrate TreeSet 
import java.util.*; 

class TreeSetExample { 

	public static void main(String[] args) 
	{ 
		TreeSet<String> ts1 = new TreeSet<String>(); 

		// Elements are added using add() method 
		ts1.add("A"); 
		ts1.add("B"); 
		ts1.add("C"); 

		// Duplicates will not get insert 
		ts1.add("C"); 

		// Elements get stored in default natural 
		// Sorting Order(Ascending) 
		System.out.println(ts1); 
	} 
} 

[A, B, C]
```

Methods: 
-   add(), contains(), first()- print first element, last()- print last element, remove()

Iterate by For loop:
    // Iterating though the TreeSet 
    TreeSet<String> ts = new TreeSet<String>(); 
        for (String value : ts) 
            System.out.print(value + ", "); 

```
TreeSet<StringBuffer> ts 
            = new TreeSet<StringBuffer>(); 
  
        // Elements are added using add() method 
        ts.add(new StringBuffer("A")); 
        ts.add(new StringBuffer("Z")); 
        ts.add(new StringBuffer("L")); 
        ts.add(new StringBuffer("B")); 
        ts.add(new StringBuffer("O")); 
  
        // We will get RunTimeException :ClassCastException 
        // As StringBuffer does not 
        // implements Comparable interface 
        System.out.println(ts); 
```

Error: ClassCastException   
String class and all the Wrapper classes already implements Comparable interface but StringBuffer class doesn’t implements Comparable interface. Hence, we get a ClassCastException in the above example

- From JDK 7 onwards, null is not at all accepted by TreeSet
- Best for storing large amount of data, faster access and retrival time.
- The insertion of null values into a TreeSet throws NullPointerException because while insertion of null, it gets compared to the existing elements and null cannot be compared to any value.

How does TreeSet work Internally?

- Implemenation of self-balancing tree . Operations like add, remove and search : O(logN)
- This is considered as one of the most efficient data structure in order to store the huge sorted data and perform operations on it. However, operations like printing N elements in the sorted order takes O(N) time.

Synchronized TreeSet

-   TreeSet ts = new TreeSet();
    Set syncSet = Collections.synchronziedSet(ts); 

### LinkedHashSet 

- Insertion ordered maintained
- No Duplicates. Contains unique elements only like HashSet
- Syntax: LinkedHashSet<String> hs = new LinkedHashSet<String>();

Internal working of Set/HashSet:

- It uses HashMap as internal working
    public boolean add(E e) {
        return map.put(e, PRESENT)==null;
    }

Merge two sets in Java

Input : a = [1, 3, 5, 7, 9]
        b = [0, 2, 4, 6, 8]
Output : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

```
    // Creating an empty set 
        Set<T> mergedSet = new HashSet<T>(); 
        // add the two sets to be merged 
        // into the new set 
        mergedSet.addAll(a); 
        mergedSet.addAll(b); 
```

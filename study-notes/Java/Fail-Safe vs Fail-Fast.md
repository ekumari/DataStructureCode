## Fail Fast & Fail Safe(Non Fail Fast)

**ConcurrentModification**: Modify a collection when other thread iterating over it.

Some iterator throws ConcurrentModificationException.

* Fail-Fast iterators immediately throw ConcurrentModificationException if there is structural modification( means adding, removing or updating any element from collection while a thread is iterating over that collection) of the collection.
* Fail-Safe iterators don’t throw any exceptions if a collection is structurally modified while iterating over it. Because, they operate on the clone of the collection. E.g: CopyOnWriteArrayList, ConcurrentHashMap.

### How Fail Fast Iterator works ?

Fail Fast Iterator uses an internal flag called as modCount which is updated each time when collection is modified. Fail-fast iterators checks the modCount flag whenever it gets the next value (i.e. using next() method), and if it finds that the modCount has been modified after this iterator has been created, it throws ConcurrentModificationException.

```
// Java code to illustrate 
// Fail Fast Iterator in Java 
import java.util.HashMap; 
import java.util.Iterator; 
import java.util.Map; 

public class FailFastExample { 
	public static void main(String[] args) 
	{ 
		Map<String, String> cityCode = new HashMap<String, String>(); 
		cityCode.put("Delhi", "India"); 
		cityCode.put("Moscow", "Russia"); 
		cityCode.put("New York", "USA"); 

		Iterator iterator = cityCode.keySet().iterator(); 

		while (iterator.hasNext()) { 
			System.out.println(cityCode.get(iterator.next())); 

			// adding an element to Map 
			// exception will be thrown on next call 
			// of next() method. 
			cityCode.put("Istanbul", "Turkey"); 
		} 
	} 
} 
```
Output:

India
Exception in thread "main" java.util.ConcurrentModificationException
    at java.util.HashMap$HashIterator.nextNode(HashMap.java:1442)
    at java.util.HashMap$KeyIterator.next(HashMap.java:1466)
    at FailFastExample.main(FailFastExample.java:18)


Note 2 : If you remove an element via Iterator remove() method, exception will not be thrown. However, in case of removing via a particular collection remove() method, ConcurrentModificationException will be thrown. 

```
Iterator<Integer> itr = al.iterator(); 
        while (itr.hasNext()) { 
            if (itr.next() == 2) { 
                // will not throw Exception 
                itr.remove(); 
            } 
        } 
  
System.out.println(al); 
  
itr = al.iterator(); 
        while (itr.hasNext()) { 
            if (itr.next() == 3) { 
                // will throw Exception on 
                // next call of next() method 
                al.remove(3); 
            } 
        } 
```

**Fail Safe**: Make copy of collection and iterates over the copied collection. Any affects the copied collection, not the original collection. So, original collection remains structurally unchanged. 
- Dont throw any Exception
- E.g: CopyOnWriteArrayList, ConcurrentHashMap.
- ConcurrentHashMap- No need to create copy but still it works with iterating over the original collection without any exception.

```
// Java code to illustrate 
// Fail Safe Iterator in Java 
import java.util.concurrent.CopyOnWriteArrayList; 
import java.util.Iterator; 

class FailSafe { 
	public static void main(String args[]) 
	{ 
		CopyOnWriteArrayList<Integer> list 
			= new CopyOnWriteArrayList<Integer>(new Integer[] { 1, 3, 5, 8 }); 
		Iterator itr = list.iterator(); 
		while (itr.hasNext()) { 
			Integer no = (Integer)itr.next(); 
			System.out.println(no); 
			if (no == 8) 

				// This will not print, 
				// hence it has created separate copy 
				list.add(14); 
		} 
	} 
} 
```
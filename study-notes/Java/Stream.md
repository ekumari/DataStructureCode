## STREAM API IN JAVA

Introduced in Java 8, It is used to process collections of objects.
A stream is a sequence of objects that supports various methods which can be pipelined to produce the desired result.

### features of Java stream are :
-   A stream is not a data structure instead it takes input from the Collections, Arrays or I/O channels
-   Streams don’t change the original data structure, they only provide the result as per the pipelined methods.
- Each intermediate operation is lazily executed and returns a stream as a result, hence various intermediate operations can be pipelined. Terminal operations mark the end of the stream and return the result.
-  Stream is used to compute elements as per the pipelined methods without altering the original value of the object.
### Intermediate Operations:

1. map: Returns a stream consisting of the results of applying the given function to the elements of this stream.

    List number = Arrays.asList(2,3,4,5);
    List square = number.stream().map(x->x*x).collect(Collectors.toList());

2. filter: It is used to select elements as per the Predicate passed as argument.
    
    List names = Arrays.asList("Reflection","Collection","Stream");
    List result = names.stream().filter(s->s.startsWith("S")).collect(Collectors.toList());

3. sorted: Sort the stream

    List names = Arrays.asList("Reflection","Collection","Stream");
    List result = names.stream().sorted().collect(Collectors.toList());

### Terminal Operations:

1. collect: Return result of intermediate operations performed on the stream.
    
    List number = Arrays.asList(2,3,4,5,3);
    Set square = number.stream().map(x->x*x).collect(Collectors.toSet());

2. forEach: It is used to iterate through every element of the stream.

    List number = Arrays.asList(2,3,4,5);
    number.stream().map(x->x*x).forEach(y->System.out.println(y));

3. reduce: It is used to reduce the elements of a stream to a single value.

    List number = Arrays.asList(2,3,4,5);
    int even = number.stream().filter(x->x%2==0).reduce(0,(ans,i)-> ans+i);


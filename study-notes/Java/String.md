## Strings

Immutable that cannot be changed.

## Ways to create string

- String Literals
    ```
    String str = "Anjani";
    ```
- Using new keyword
    ```
    String str = new String("Anjani");
    ```

## Methods that String has..

```
public static void main (String[] args) 
    { 
        String s= "GeeksforGeeks"; 
        // or String s= new String ("GeeksforGeeks"); 
  
        // Returns the number of characters in the String. 
        System.out.println("String length = " + s.length()); 
  
        // Returns the character at ith index. 
        System.out.println("Character at 3rd position = "
                           + s.charAt(3)); 
  
        // Return the substring from the ith  index character 
        // to end of string 
        System.out.println("Substring " + s.substring(3)); 
  
        // Returns the substring from i to j-1 index. 
        System.out.println("Substring  = " + s.substring(2,5)); 
  
        // Concatenates string2 to the end of string1. 
        String s1 = "Geeks"; 
        String s2 = "forGeeks"; 
        System.out.println("Concatenated string  = " + 
                            s1.concat(s2)); 
  
        // Returns the index within the string 
        // of the first occurrence of the specified string. 
        String s4 = "Learn Share Learn"; 
        System.out.println("Index of Share " +  
                           s4.indexOf("Share")); 
  
        // Returns the index within the string of the 
        // first occurrence of the specified string, 
        // starting at the specified index. 
        System.out.println("Index of a  = " +  
                           s4.indexOf('a',3)); 
  
        // Checking equality of Strings 
        // It compares Values
        Boolean out = "Geeks".equals("geeks"); 
        System.out.println("Checking Equality  " + out); //false
        out = "Geeks".equals("Geeks"); 
        System.out.println("Checking Equality  " + out); // true
  
        out = "Geeks".equalsIgnoreCase("gEeks "); 
        System.out.println("Checking Equality " + out);  // true
          
        //If ASCII difference is zero then the two strings are similar 
        int out1 = s1.compareTo(s2); 
        System.out.println("the difference between ASCII value is="+out1); 
        // Converting cases 
        String word1 = "GeeKyMe"; 
        System.out.println("Changing to lower Case " + 
                            word1.toLowerCase()); 
  
        // Converting cases 
        String word2 = "GeekyME"; 
        System.out.println("Changing to UPPER Case " +  
                            word2.toUpperCase()); 
  
        // Trimming the word 
        String word4 = " Learn Share Learn "; 
        System.out.println("Trim the word " + word4.trim()); 
  
        // Replacing characters 
        String str1 = "feeksforfeeks"; 
        System.out.println("Original String " + str1); 
        String str2 = "feeksforfeeks".replace('f' ,'g') ; 
        System.out.println("Replaced f with g -> " + str2); 
    }  
```
## Output

```
String length = 13
Character at 3rd position = k
Substring ksforGeeks
Substring = eks
Concatenated string = GeeksforGeeks
Index of Share 6
Index of a = 8
Checking Equality false
Checking Equality true
Checking Equality false
the difference between ASCII value is=-31
Changing to lower Case geekyme
Changing to UPPER Case GEEKYME
Trim the word Learn Share Learn
Original String feeksforfeeks
Replaced f with g -> geeksgorgeeks
```

## How to Initialize and Compare Strings in Java?
### String Literals
-   String str = "GeeksForGeeks"

    String constant will be created and stored in string pooled inside heap area of memory.

    String str = “GeeksForGeeks”; 

![image info](..\images\StringConstantPool.png
)

    str = “geeks”;
![image info](..\images\StringConstantPool2.png
)  

**Note** If we again write str = “GeeksForGeeks” as next line, then it first check that if given String constant is present in String pooled area or not. If it present then str will point to it, otherwise creates a new String constant. 

### Object Initialization(Dynamic)
-   String str = new String("very");

    String object will be created in heap area (not inside the string constant pool). Also, with same value, a String constant is also created in String pool area, but the variable will point to String object in heap area.

    ![image info](..\images\StringNewObject.png)

    str = “good”;

    ![image info](..\images\StringNewObject2.png)  

**Note** If we again write str = new String(“very”), then it will create a new object with value “very”, rather than pointing to the available objects in heap area with same value.But if we write str = “very”, then it will point to String constant object with value “very”, present in String pooled area.

### Comparing Strings and their References

1.  equals() - It compares values as it is overriden by String class and provided its own implementation of comparing values rather than reference.

2.  == opeartor - It compares references not values. 

3. compareTo() method - It compares values lexicographically and returns an integer value.
```
str1 == str2 : return 0
str1 > str2 : return a positive value
str1 < str2 : return a negative value
```

**Example**
```
        String s1 = "Ram"; 
        String s2 = "Ram"; 
        String s3 = new String("Ram"); 
        String s4 = new String("Ram"); 
        String s5 = "Shyam"; 
        String nulls1 = null; 
        String nulls2 = null; 
  
        System.out.println(" Comparing strings with equals:"); 
        System.out.println(s1.equals(s2)); 
        System.out.println(s1.equals(s3)); 
        System.out.println(s1.equals(s5)); 
        // System.out.println(nulls1.equals(nulls2));  // NullPointerException 
  
        System.out.println(" Comparing strings with ==:"); 
        System.out.println(s1 == s2); 
        System.out.println(s1 == s3); 
        System.out.println(s3 == s4); 
        System.out.println(nulls1 == nulls2); 
  
        System.out.println(" Comparing strings with compareto:"); 
        System.out.println(s1.compareTo(s3)); 
        System.out.println(s1.compareTo(s5)); 
  
```
**Output**
```
String s1 = "Ram"; 
        String s2 = "Ram"; 
        String s3 = new String("Ram"); 
        String s4 = new String("Ram"); 
        String s5 = "Shyam"; 
        String nulls1 = null; 
        String nulls2 = null; 
  
        System.out.println(" Comparing strings with equals:"); 
        System.out.println(s1.equals(s2)); 
        System.out.println(s1.equals(s3)); 
        System.out.println(s1.equals(s5)); 
        // System.out.println(nulls1.equals(nulls2));  // NullPointerException 
  
        System.out.println(" Comparing strings with ==:"); 
        System.out.println(s1 == s2); //true 
        System.out.println(s1 == s3); //false
        System.out.println(s3 == s4); //false
        System.out.println(nulls1 == nulls2); //true 
  
        System.out.println(" Comparing strings with compareto:"); 
        System.out.println(s1.compareTo(s3)); 
        System.out.println(s1.compareTo(s5)); 
```

## StringBuffer

- It is mutable which means its value can be changed. 
- It is synchronized means thread safe.

### Declaration
```
StringBuffer s=new StringBuffer("Geeksfor");
```
### Some Imp Methods

- s.length()
- s.capacity()
- s.append("Geeks") : GeeksforGeeks
- s.insert(5,"for") : Insert text at specified position.
- s.reverse(): Reverse the string e.g rofskeeG 
- s.delete()
- s.deleteCharAt(loc)
- s.replace(int startIndex, int endIndex, String str)

### Interesting Facts
* public final class StringBuffer extends Object implements Serializable, CharSequence, Appendable
* String buffers are safe for use by multiple threads
* Inherit some methods from Object class are clone, equals, finilize, hashCode, notify and notifyAll.

## String Builder

Java5 adds a new String class called String Builder which is same as String Buffer except it is not synchronized i.e thread safe.

*  String Builder is faster and preferred over String Buffer for single thread program.
* If thread safe is needed then use StringBuffer.

## String Joiner

Helps in joining the string
```
Syntax : 

public StringJoiner(CharSequence delimiter)

Parameters : 
delimiter - the sequence of characters to be used between each element added to the StringJoiner value

Throws:
NullPointerException - if delimiter is null
```

### Code:

```
 public static void main(String[] args) 
    { 
       ArrayList<String> al = new ArrayList<>(); 
         
       al.add("Ram"); 
       al.add("Shyam"); 
       al.add("Alice"); 
       al.add("Bob"); 
         
       StringJoiner sj1 = new StringJoiner(","); 
         
       // setEmptyValue() method 
       sj1.setEmptyValue("sj1 is empty"); 
       System.out.println(sj1); 
         
       // add() method 
       sj1.add(al.get(0)).add(al.get(1)); 
       System.out.println(sj1); 
         
       // length() method 
       System.out.println("Length of sj1 : " + sj1.length()); 
         
       StringJoiner sj2 = new StringJoiner(":"); 
       sj2.add(al.get(2)).add(al.get(3)); 
         
       //merge() method 
       sj1.merge(sj2); 
         
       // toString() method 
       System.out.println(sj1.toString()); 
         
       System.out.println("Length of new sj1 : " + sj1.length()); 
      
    } 
```
### Output

```
sj1 is empty
Ram,Shyam
Length of sj1 : 9
Ram,Shyam,Alice:Bob
Length of new sj1 : 19
```

## Conversion From StringBuilder,StringBuffer to String

```
StringBuffer str = new StringBuffer();
String S = str.toString();
```

## Conversion From StringBuilder,StringBuffer to String
```
String S = "ANJANI";
StringBuffer str = new StringBuffer(S);
```

## When to use StringJoiner over StringBuilder?

String Joiner is important when you need to join Strings in a Stream.

**Task**: Given String Array ["George","Sally","Fred"] 
Convert to String [George:Sally:Fred]?

```
 public static void main(String[] args) 
    { 
        // given string array 
        String str[] = {"George","Sally","Fred"}; 
              
        // By using StringJoiner class 
              
        // initializing StringJoiner instance with 
        // required delimiter, prefix and suffix 
        StringJoiner sj = new StringJoiner(":", "[", "]"); 
              
        // concatenating strings 
        sj.add("George").add("Sally").add("Fred"); 
              
        // converting StringJoiner to String 
        String desiredString = sj.toString(); 
              
        System.out.println(desiredString); 
              
        // By using StringBuilder class 
              
        // declaring empty stringbuilder 
        StringBuilder sb = new StringBuilder(); 
              
        // appending prefix 
        sb.append("["); 
              
        // cheking for empty string array 
        if(str.length>0) 
        { 
            // appending first element 
            sb.append(str[0]); 
                  
            // iterating through string array  
            // and appending required delimiter 
            for (int i = 1; i < str.length; i++)  
            { 
                sb.append(":").append(str[i]); 
            } 
        } 
              
        // finally appending sufix 
        sb.append("]"); 
              
        // converting StringBuilder to String 
        String desiredString1 = sb.toString(); 
              
        System.out.println(desiredString1); 
    } 
```

**Output**
```
[George:Sally:Fred]
[George:Sally:Fred]
```

**Conclustion** StringBuilder is lengthy work in previour program. StringJoiner is faster for joining or concating.

### Convert any data type to String
-   Using toString(), or String.valueOf(datatype)

### String to Integer in Java – parseInt()

Sometimes, we need to convert number represent as String to Integer type.

-   Using parseInt() method - we can convert it but it throws **NumberFormatExceptio** exception. Because, value represented by String is not a number.

## Method To Use In Programming

* Swap two String without third variable: Use Concat and SubString
* Searching in a String: Use indexOf(), lastIndexOf()
* Compare String - compareTo(str1,str2), check character by character, str1.equals(str2), 

**Imp** == checks if both objects point to the same memory location whereas .equals() evaluates to the comparison of values in the objects.

```
        String s1 = new String("HELLO"); 
        String s2 = new String("HELLO"); 
  
        System.out.println(s1 == s2); 
  
        System.out.println(s1.equals(s2)); 
```
Output:
```
false
true
```

Q.Counting number of lines, words, characters and paragraphs in a text file using Java?

https://www.geeksforgeeks.org/counting-number-lines-words-characters-paragraphs-text-file-using-java/

Q. Check if a string contains only alphabets in Java using Lambda expression?

```
public static boolean isStringOnlyAlphabet(String str) 
{ 
    return ((!str.equals("")) 
            && (str != null) 
            && (str.chars().allMatch(Character::isLetter))); 
} 
```
Q.Check if a string contains only alphabets in Java using ASCII values?
```
public static boolean isStringOnlyAlphabet(String str) 
{ 
    if (str == null || str.equals("")) { 
        return false; 
    } 
    for (int i = 0; i < str.length(); i++) { 
        char ch = str.charAt(i); 
        if ((!(ch >= 'A' && ch <= 'Z')) 
            && (!(ch >= 'a' && ch <= 'z'))) { 
            return false; 
        } 
    } 
    return true; 
} 
```
*Using Regex*

```
public static boolean isStringOnlyAlphabet(String str) 
{ 
    return ((!str.equals("")) 
            && (str != null) 
            && (str.matches("^[a-zA-Z]*$"))); 
} 
```
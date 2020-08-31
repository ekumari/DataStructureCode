## File

- java.io package
- Representation of a file and directory path name
- First of all, We create file class object by passing the filename or directory name to it. 
- Instance of file class is immutable, that once created, the abstract pathname represented by a File object will never change.

### How to create a File Object?

File a = new File("/usr/local/bin/geeks");

### Different ways of Reading a text file in Java

- FileReader
- BufferedReader: Buffering of data for fast reading
- Scanner: Parsing ability
- Stream: JAVA 8 provides Stream, which provides lazyy and more efficient way to read a file.

**FileReader**: Read character by character
```
FileReader fr = 
      new FileReader("C:\\Users\\pankaj\\Desktop\\test.txt"); 
  
    int i; 
    while ((i=fr.read()) != -1) 
      System.out.print((char) i); 
```
**Scanner class**: Read word by word, A Scanner breaks its input into tokens using a delimiter pattern, which by default matches whitespace.The resulting tokens may then be converted into values of different types using the various next methods

```
// pass the path to the file as a parameter 
    File file = 
      new File("C:\\Users\\pankaj\\Desktop\\test.txt"); 
    Scanner sc = new Scanner(file); 
  
    while (sc.hasNextLine()) 
      System.out.println(sc.nextLine()); 
```

**BufferedReader**: Read characters, lines and arrays

```
File file = new File("C:\\Users\\pankaj\\Desktop\\test.txt"); 
  
  BufferedReader br = new BufferedReader(new FileReader(file)); 
  
  String st; 
  while ((st = br.readLine()) != null) 
    System.out.println(st); 
  } 
```

### Java program to delete certain text or lines from a file 

Prerequisite : PrintWriter , BufferedReader

Given two files input.txt and delete.txt. Our Task is to perform file extraction(Input-Delete) and save the output in file say output.txt

![image info](..\images\fileextraction.jpeg
)  

1. Create PrintWriter object for output.txt
2. Open BufferedReader for input.txt
3. Run a loop for each line of input.txt
   3.1 flag = false
   3.2 Open BufferedReader for delete.txt
   3.3 Run a loop for each line of delete.txt
      ->  If  line of delete.txt is equal to current line of input.txt 
            -> flag = true
            -> break loop

4. Check flag, if false
     -> write current line of input.txt to output.txt
5. Flush PrintWriter stream and close resources.

A better solution is to use HashSet to store each line of delete.txt and then while looping through lines of input.txt ,check if it is in hashset. If not present, write that line into output.txt.

```
 // PrintWriter object for output.txt 
        PrintWriter pw = new PrintWriter("output.txt"); 
          
        // BufferedReader object for delete.txt 
        BufferedReader br2 = new BufferedReader(new FileReader("delete.txt")); 
          
        String line2 = br2.readLine(); 
          
        // hashset for storing lines of delete.txt 
        HashSet<String> hs = new HashSet<String>(); 
          
        // loop for each line of delete.txt 
        while(line2 != null) 
        { 
            hs.add(line2); 
            line2 = br2.readLine(); 
        } 
                      
        // BufferedReader object for input.txt 
        BufferedReader br1 = new BufferedReader(new FileReader("input.txt")); 
          
        String line1 = br1.readLine(); 
          
        // loop for each line of input.txt 
        while(line1 != null) 
        { 
            // if line is not present in delete.txt 
            // write it to output.txt 
            if(!hs.contains(line1)) 
                pw.println(line1); 
              
            line1 = br1.readLine(); 
        } 
          
        pw.flush(); 
          
        // closing resources 
        br1.close(); 
        br2.close(); 
        pw.close(); 
          
        System.out.println("File operation performed successfully");  
```

### Delete a file using Java

File file = new File("C:\\Users\\Mayank\\Desktop\\1.txt"); 
          
        if(file.delete())  // delete method to delete file
        { 
            System.out.println("File deleted successfully"); 
        } 

Files.deleteIfExists(Paths.get("C:\\Users\\Mayank\\Desktop\\ 
            445.txt")); 



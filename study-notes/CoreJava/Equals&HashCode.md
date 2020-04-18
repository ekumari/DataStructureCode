## Equals & HashCode 

### Equals

* Compare two object if they are equal or not - w.r.t content
* Implementaion of equals method in object class, only check the two objects refer to the same objects or not.
* By default, we get the default implementation of equals method. 

### HashCode() method

*   Returns a hash code ( an integer value)
*   Helps to identify an object in the heap of other objects
* Helps in Improving collection performance, collection look for an object as fast as possible.

### Example of equals()
```
Student class which takes the student registration number.
Registration num is unique to each student.

Student s = new Student("H234");
Student s2 = new Student("H234"); 
```

Same student but different objects

Main moto of equals method to confirm that these two objects are same with respect to data.

```
equals provided by object class returns false.

s.equals(s2); - returns false 

Object implementation of equals only checks object reference which is s and s2. They are not same.
It is not looking at internal data.
```
```
Map<Student, ReportCard> studentReport = new HashMap<>();
studentReport.put(s, new ReportCard());
studentReport.put(s2, new ReportCard());

studentReport.size() - 2 but they are same so it should be 1.
```
Need to implement equals and hashCode method for better performance of HashMap.

```
public boolean equals(Object o){
    if(o!=null && o instanceof Student){
        String regNumber = ((Stduent)o).getRegistrationNumber();
        if(regNumber != null && regNumber.equals(this.getRegistrationNumber())){
            return true;
        }
    }
        return false;
}

public int hashCode(){
    return this.registrationNumber.hashCode();  
}
```
studentReport.size() - returns 1 which is correct
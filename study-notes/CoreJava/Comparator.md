## Comparable Vs Comparator

## Collections.sort(list) 
    It works with list only. For hashmap sorting, you convert the hashmap to list and use collection.sort(list, comparator) then store the sorted data back to hashmap.

### Comparable

Create a list of values-

List<String> names = new ArrayList<>();
*   When we have list of integer/string, we can easily sort them by Collection.sort(names);

List<Laptop> laps = new ArrayList<>();
*   List of User defined object will not work with Collection.sort(laps); 
* Collection becomes confuse as on which parameter it has to sort the values (brand, price or ram)?

*   If you want to sort the list of object then you have implements Comparable and it has compareTo(obj) method.
* Override compareTo method 
* Collection.sort() - Example of abstraction, as you don't know which algorithm is being used by java for sorting.

```
public class Laptop implements Comparable<Laptop>{
    private String brand;
    private int ram;
    private int price;

    constructor
    Getter & Setter for data member
    to String method

    @Override
    public int compareTo(Laptop lap2){
        //Logic when to swap
        <!-- this > lap2 = +
        this < lap2 = -
        this == lap2 = 0  -->

        if(this.getPrice() > o.getPrice()){
            return 1;
        }else{
            return -1;
        }
    }
    

}

public class Runner{
    public static void main(){
        List<Laptop> laps = new ArrayList<>();
        laps.add("Dell",16,800);
        laps.add("Apple",8,1200);
        laps.add("Acer",12,700);

        Collections.sort(laps); Sorted based on price
    }
}
```
### Comparator

When to use Comparator: 

1. Let's say Laptop is a third party library and you can't change the source code to add sorting logic as we have done above.
So Collection.sort is interested in logic which we can provide by comparator interface.
Collections.sort(list, comparator obj);

2. Sort based on some other parameter


```
public class Runner{
    public static void main(){
        List<Laptop> laps = new ArrayList<>();
        laps.add("Dell",16,800);
        laps.add("Apple",8,1200);
        laps.add("Acer",12,700);

        Comparator<Laptop> com = new Comparator<Laptop>(){
            public int compare(Laptop l1, Laptop l2){
                if(l1.getRam > l2.getRam())
                    return 1;
                else
                    return -1;
            }
        }
        Collections.sort(laps, com); Sorted based on ram using comparator
    }
}
```
### Conclusion

1. When your class is not implementing comparable
2. When you want to change the way it's sort the values.

All the inbuilt classes in java (String, Integer) implements Comparable but by default they have their own logic, but if you want your logic then in that case, use Comparator
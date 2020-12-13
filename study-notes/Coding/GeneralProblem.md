## Bit Manipulation Question
---

- Last bits is 0 -> even
- Last bits is 1 -> odd

Q. To find even number?
- return n&1; -> if n's last bit 0 then 0&1 -> return 0 -> means even
- return n&1; -> if n's last bit 1 then 1&1 -> return 1 -> means odd

a = 5 (101)
b = 7 (111)
&
-----------
5     (101)


Q. Power of 2 and Count no of 1 bits
- return (x!=0) && (x & (x-1)) == 0;
- count=0, while (x!=0){ (x & (x-1)) == 0; count++ } -> Count nos of 1 bit

## String
---

Decimal -> Roman

1904 -> MCMIV

Step1: Create function say "value(int)" which will return roman number. 1-> I, 4- IV, 5-V etc

Step2: Bases Array store [1000,900,500,400,100,90,50,40,10,9,4,5,1]

Two Loops:

n=1904, result = "";
```
for(int i: Bases){
    while(n >=i){
        result+=value(i);
        n=n-i;
    }
}
```

Return result

## Array
---

Q. Find Duplicate in array?

Arr = [3,4,1,4,1]

Approach1: Use set collection, if set contains the data then it returns false. 

Approach2: Using negate ways

For e.g
- i=0, A[i] = 3 then check A[3] < 0 if yes then A[i] is duplicate

[3,-4,1,-4,-1] -> 4,1

## Permutation & Combinations
---
 **Combinations:** All the different ways in which we can group something, where order doesn't matter.

 [A,B,C] in 1 place- only one combination [ABC]

 [A,B,C] in 2 place- [AB] [BC] [AC]

 ABC,ACB are all same, here order doesnt matter.


 **Permutation:** All the different ways in which we can group something, where order does matter.

[A,B,C] in 2 place- [AB] [AC] [BA] [BC] [CA] [CB]

 0,1 in 3 bits -> 2^3 = 8 permutation

 Note: Solve problems in loops
 

 ---------------------

Moore's voting algo:

- Application: Majority Element, Repeat number n/3(based on but with more modification) , n/2


    Approach: This is a two-step process. 
        The first step gives the element that maybe the majority element in the array. If there is a majority element in an array, then this step will definitely return majority element, otherwise, it will return candidate for majority element.
        Check if the element obtained from the above step is majority element. This step is necessary as there might be no majority element.
         
    Algorithm: 
        Loop through each element and maintains a count of majority element, and a majority index, maj_index
        If the next element is same then increment the count if the next element is not same then decrement the count.
        if the count reaches 0 then changes the maj_index to the current element and set the count again to 1.
        Now again traverse through the array and find the count of majority element found.
        If the count is greater than half the size of the array, print the element
        Else print that there is no majority element

Pigenhole Sorting:






## Minimum Number of Platforms Required for a Railway/Bus Station

O(nlogn) + O(n)

    Input: arr[] = {9:00, 9:40, 9:50, 11:00, 15:00, 18:00}
    dep[] = {9:10, 12:00, 11:20, 11:30, 19:00, 20:00}
    Output: 3
    Explantion: There are at-most three trains at a time (time between 11:00 to 11:20)

    Input: arr[] = {9:00, 9:40}
    dep[] = {9:10, 12:00}
    Output: 1
    Explantion: Only one platform is needed. 


Algo:
1. Sort arrival and depart arrays
    Collections.sort(arrival);
    Collections.sort(depart);
2. Merge sort  
```
    while(i<size && j<size)
         if arrival[i] <= depart[j] then plat_needed++, i++;
         else if arrival[i] > depart[j] then plat_needed--, j++;

         if(plat_needed > result)
         result = plat_needed;


Return result
```

## Rotate Matrix

1.A= [ 1,2,3
     4,5,6
     7,8,9 ]


Approach: 

* Transpose the matrix means A[i][j] = A[j][i]

```
for i = 0 to length-1
    for j = i to length-1 // should start with j = i bcs already done the swap 0,1 to 1,0 in first loop, next time when i = 1 again it will swap 1,0 to 0,1

        temp = A[i][j];
        A[i][j]=A[j][i];
        A[j][i]=temp;
```

* Reverse horizontally using two pointer

```
    for i = 0 to length-1 // traverse to all rows
        for i = 0 to length/2  // go till half column
            temp = A[i][j]; //first element
            A[i][j] = A[i][length-1-j]; // last element
            A[i][length-1-j] = A[i][j];
```

* ArrayList 

```
    int temp = a.get(i).get(j);
    a.get(i).set(j,a.get(j).get(i));
    a.get(j).set(i, temp);
```

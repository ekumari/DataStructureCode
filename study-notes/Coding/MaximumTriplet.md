## Maximum Triplet Sum


Given an array A containing N integers.

You need to find the maximum sum of triplet ( Ai + Aj + Ak ) such that 0 <= i < j < k < N and Ai < Aj < Ak.

If no such triplet exist return 0.


Algorithm1:

- Choose i as middle and find max number less than Ai on left side and find max number > Ai on right side.
- Update max if left and right != 0, means there is triplet.
- Return max

O(n^2)

```
 public int solve(ArrayList<Integer> A) {
        int max = 0;
        int n = A.size();
        for (int i = 1; i < n - 1; ++i) {
            int max1 = 0, max2 = 0;
 
            for (int j = 0; j < i; ++j)
                if (A.get(j) < A.get(i))
                    max1 = Math.max(max1, A.get(j));
 
            for (int j = i + 1; j < n; ++j)
                if (A.get(j) > A.get(i))
                    max2 = Math.max(max2, A.get(j));
 
            // store maximum answer
         if(max1!=0 && max2!=0)
            max = Math.max(max, max1 + A.get(i) + max2);
        }
        
        return max;
    }
```

Algo2: Better Solution O(nlogn)
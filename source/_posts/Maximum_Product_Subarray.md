title: Maximum Product Subarray
date: 2016-02-14 19:26:16
categories:
- Leetcode
tags:
- Leetcode
- Array
- Dynamic Programming
comments: true
---

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.

```java
public class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length < 1)return 0;
        
        int maxEndHerePrev = nums[0], minEndHerePrev = nums[0], maxSoFar = nums[0]
        // interleaving in the following equations
        int maxEndHere = nums[0], minEndHere = nums[0];
        
        for(int i = 1; i < nums.length; i++){
            maxEndHere = Math.max(nums[i], Math.max(maxEndHerePrev * nums[i], minEndHerePrev * nums[i]));
            minEndHere = Math.min(nums[i], Math.min(maxEndHerePrev * nums[i], minEndHerePrev * nums[i]));
            maxSoFar = Math.max(maxEndHere, maxSoFar);
            maxEndHerePrev = maxEndHere;
            minEndHerePrev = minEndHere;
        }
        return maxSoFar;
    }
}
```

Another solution from this [post](https://leetcode.com/discuss/14235/possibly-simplest-solution-with-o-n-time-complexity)

```java
int maxProduct(int A[], int n) {
    // store the result that is the max we have found so far
    int r = A[0];

    // imax/imin stores the max/min product of
    // subarray that ends with the current number A[i]
    for (int i = 1, imax = r, imin = r; i < n; i++) {
        // multiplied by a negative makes big number smaller, small number bigger
        // so we redefine the extremums by swapping them
        if (A[i] < 0)
            swap(imax, imin);

        // max/min product for the current number is either the current number itself
        // or the max/min by the previous number times the current one
        imax = max(A[i], imax * A[i]);
        imin = min(A[i], imin * A[i]);

        // the newly computed max value is a candidate for our global result
        r = max(r, imax);
    }
    return r;
}
```
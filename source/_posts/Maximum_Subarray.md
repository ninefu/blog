title: Maximum Subarray
date: 2016-02-13 22:28:52
categories:
- Leetcode
tags:
- Leetcode
- Array
- Dynamic Programming
- Divide and Conquer
comments: true
---

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [−2,1,−3,4,−1,2,1,−5,4],
the contiguous subarray [4,−1,2,1] has the largest sum = 6.


### DP solution, O(n) time

> this problem was discussed by Jon Bentley (Sep. 1984 Vol. 27 No. 9 Communications of the ACM P885)

> the paragraph below was copied from his paper (with a little modifications)

> algorithm that operates on arrays: it starts at the left end (element A[1]) and scans through to the right end (element A[n]), keeping track of the maximum sum subvector seen so far. The maximum is initially A[0]. Suppose we've solved the problem for A[1 .. i - 1]; how can we extend that to A[1 .. i]? The maximum sum in the first I elements is either the maximum sum in the first i - 1 elements (which we'll call MaxSoFar), or it is that of a subvector that ends in position i (which we'll call MaxEndingHere).

> MaxEndingHere is either A[i] plus the previous MaxEndingHere, or just A[i], whichever is larger.

```java
public int maxSubArray(int[] A) {
        int n = A.length;
        int[] dp = new int[n];//dp[i] means the maximum subarray ending with A[i];
        dp[0] = A[0];
        int max = dp[0];

        for(int i = 1; i < n; i++){
            dp[i] = A[i] + (dp[i - 1] > 0 ? dp[i - 1] : 0);
            max = Math.max(max, dp[i]);
        }

        return max;
}
```


```java
public class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length < 1)return 0;
        
        int maxSoFar = nums[0], maxEndHere = nums[0];
        for(int i = 1; i < nums.length; i++){
            maxEndHere = Math.max(maxEndHere + nums[i], nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndHere);
        }
        
        return maxSoFar;
    }
}
```

### Divide and Conquer

From the [post](https://leetcode.com/discuss/694/how-solve-maximum-subarray-using-divide-and-conquer-approach)

> Step1. Select the middle element of the array. So the maximum subarray may contain that middle element or not.

> Step 2.1 If the maximum subarray does not contain the middle element, then we can apply the same algorithm to the the subarray to the left of the middle element and the subarray to the right of the middle element.

> Step 2.2 If the maximum subarray does contain the middle element, then the result will be simply the maximum suffix subarray of the left subarray plus the maximum prefix subarray of the right subarray

> Step 3 return the maximum of those three answer.

> The recurrence is: T(n) = 2T(n / 2) + O(1). So the running time of this algorithm is O(n).

```c++
class Solution {
public:
    int maxSubArray(int A[], int n) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        if(n==0) return 0;
        return maxSubArrayHelperFunction(A,0,n-1);
    }

    int maxSubArrayHelperFunction(int A[], int left, int right) {
        if(right == left) return A[left];
        int middle = (left+right)/2;
        int leftans = maxSubArrayHelperFunction(A, left, middle);
        int rightans = maxSubArrayHelperFunction(A, middle+1, right);
        int leftmax = A[middle];
        int rightmax = A[middle+1];
        int temp = 0;
        for(int i=middle;i>=left;i--) {
            temp += A[i];
            if(temp > leftmax) leftmax = temp;
        }
        temp = 0;
        for(int i=middle+1;i<=right;i++) {
            temp += A[i];
            if(temp > rightmax) rightmax = temp;
        }
        return max(max(leftans, rightans),leftmax+rightmax);
    }
};
```

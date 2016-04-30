title: Missing Number
date: 2016-02-29 20:35:28
categories:
- Leetcode
tags:
- Leetcode
- Array
- Math
- Bit Manipulation
comments: true
---

### Sum, O(n) time, O(1) space

```java
public class Solution {
    public int missingNumber(int[] nums) {
        if (nums == null || nums.length == 0) return -1;
        int length = nums.length;
        int sum = (0 + length) * (length + 1) / 2;
        for (int i = 0; i < length; i++){
            sum -= nums[i];
        }
        return sum;
    }
}
```

### Bit, O(n) time, O(1) space

```java
public class Solution {
    public int missingNumber(int[] nums) {
        if (nums == null || nums.length == 0) return -1;
        int xor = 0;
        for (int i = 0; i < nums.length; i++){
            xor = xor ^ i ^ nums[i];
        }
        return xor ^ nums.length;
    }
}
```

### Binary Search, O(n log n) time, O(1) space

```java
public class Solution {
    public int missingNumber(int[] nums) {
        if (nums == null || nums.length == 0) return -1;
        Arrays.sort(nums);
        // think about the boudaries
        int start = 0, end = nums.length;
        int mid = (start + end) / 2;
        while (start < end){
            if (nums[mid] == mid){
                start = mid + 1;
            }else{
                end = mid;
            }
            mid = (start + end) / 2;
        }
        return start;
    }
}
```
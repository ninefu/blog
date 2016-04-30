title: Find Peak Element
date: 2016-01-31 14:03:06
categories:
- Leetcode
tags:
- Leetcode
- Array
- Binary Search
comments: true
---

A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

### O(n) sequential scan

```java
public class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 1; i < nums.length; i++){
            if (nums[i] < nums[i - 1]){
                return i - 1;
            }
        }
        return nums.length - 1;
    }
}
```

### O(logn) iterative binary search solution

```java
public class Solution {
    public int findPeakElement(int[] nums) {
        int low = 0, high = nums.length - 1;
        
        while (low < high){
            int mid1 = (high + low) / 2;
            int mid2 = mid1 + 1;
            if (nums[mid1] > nums[mid2]){
                high = mid1;
            }else{
                low = mid2;
            }
        }
        
        return low;
    }
}
```

### O(logn) recursive binary search solution

```java
public class Solution {
    public int findPeakElement(int[] nums) {
        return find(nums, 0, nums.length - 1);
    }
    
    public int find(int[] nums, int low, int high){
        if (low == high){
            return low;
        }else{
            int mid1 = (low + high) / 2;
            int mid2 = mid1 + 1;
            if (nums[mid1] > nums[mid2]){
                return find(nums, low, mid1);
            }else{
                return find(nums, mid2, high);
            }
        }
    }
}
```
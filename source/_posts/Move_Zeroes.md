title: Move Zeroes
date: 2016-01-09 18:34:23
categories:
- Leetcode
tags:
- Leetcode
- Array
- Two Pointers
comments: true
---

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

<!--more-->

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) return;
        int insert = 0;
        
        for (int num : nums){
            if (num != 0){
                nums[insert++] = num;
            }
        }
        
        while (insert < nums.length){
            nums[insert++] = 0;
        }
    }
}
```
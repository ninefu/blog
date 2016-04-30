title: Remove Duplicates from Sorted Array
date: 2016-01-20 15:51:13
tags:
- Leetcode
- Array
- Two Pointers
comments: true
---

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

<!--more-->

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length < 1){return 0;}
        int once = 1;
        
        for (int i = 1; i < nums.length; i++){
            if (nums[i] != nums[i - 1]){
                nums[once] = nums[i];
                once++;
            }
        }
        
        return once;
    }
}
```


```java
public int removeDuplicates(int[] nums) {
    int i = 0;
    for (int n : nums)
        if (i == 0 || n > nums[i-1])
            nums[i++] = n;
    return i;
}
```
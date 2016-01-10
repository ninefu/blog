title: Remove Elements
date: 2016-01-08 17:54:48
categories:
- Leetcode
tags:
- Leetcode
- Array
- Two Pointers
comments: true
---
Given an array and a value, remove all instances of that value in place and return the new length.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

<!--more-->

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int length = nums.length, i = 0, end = length - 1;
        
        while (i <= end){
            if (nums[i] == val){
                nums[i] = nums[end];
                end--;
                length--;
            }else{
                i++;
            }
        }
        return length;
    }
}
```

Most voted solution on Leetcode

```java
int removeElement(int A[], int n, int elem) {
    int begin = 0;
    for(int i = 0; i < n; i++) {
    	if(A[i] != elem) A[begin++] = A[i];
    }
    return begin;
}
```
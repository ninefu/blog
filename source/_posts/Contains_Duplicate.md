title: Contains Duplicate
date: 2016-01-11 16:33:00
categories: 
- Leetcode
tags:
- Leetcode
- Array
- Hash
comments: true
---

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

<!--more-->

O(N<sup>2</sup>) time O(1) memory, TLE, cited from Leetcode Discussion Board

```java
public boolean containsDuplicate(int[] nums) {
	for(int i = 0; i < nums.length; i++) {
		for(int j = i + 1; j < nums.length; j++) {
			if(nums[i] == nums[j]) {
				return true;
			}
		}
	}
	return false;
}
```

O(N log N) time O(1) memory, TLE, cited from Leetcode Discussion Board

```java
public boolean containsDuplicate(int[] nums) {
	Arrays.sort(nums);
	for(int ind = 1; ind < nums.length; ind++) {
		if(nums[ind] == nums[ind - 1]) {
			return true;
		}
	}
	return false;
}
```

O(N log N) time O(1) memory

```java
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < nums.length; i++){
            if (!set.add(nums[i])){
                return true;
            }
        }
        return false;
    }
}
```
title: Contains Duplicate II
date: 2016-01-11 18:39:45
categories:
- Leetcode
tags:
- Leetcode
- Array
- Hash
comments: true
---
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

<!--more>

#### HashMap

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap<Integer, Integer>();
        
        for (int i = 0; i < nums.length; i++){
            if (map.containsKey(nums[i])){
                if ((i - map.get(nums[i])) <= k){return true;}
            }
            map.put(nums[i],i);
        }
        return false;
    }
}
```

#### HashSet
Cited from Leetcode Discussion board

```java
public class Solution {
	public boolean containsNearbyDuplicate(int[] nums, int k) {
		Set<Integer> set = new HashSet<Integer>();
		for(int i = 0; i < nums.length; i++){
			if(i > k) set.remove(nums[i-k-1]);
			if(!set.add(nums[i])) return true;
		}
		return false;
	}
}
```
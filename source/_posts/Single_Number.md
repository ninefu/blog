title: Single Number
date: 2016-01-03 10:37:39
categories:
- Leetcode
tags:
- Leetcode
- Hash
- Bit
---
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

<!--more-->

#### O(n) time, O(n) space

```
public class Solution {
    public int singleNumber(int[] nums) {
        HashSet<Integer> set = new HashSet<Integer>();
        
        for (int i = 0; i < nums.length; i++){
            if (!set.add(nums[i])){
                set.remove(nums[i]);
            }
        }
        Object[] array = set.toArray();
        return (int) array[0];
    }
}
```

#### O(n) time, O(1) space

```java
public class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int i = 0; i < nums.length; i++){
            res ^= nums[i];
        }
        return res;
    }
}
```
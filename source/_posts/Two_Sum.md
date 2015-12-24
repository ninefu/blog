title: Two Sum
date: 2015-12-22 15:51:07
categories:
- Leetcode
tags:
- Leetcode
- Array
- Hash
comments: true
---
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2

<!--more-->

#### O(n) time, O(n) space
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[]{-1,-1};
        if (nums == null || nums.length < 2){return res;}
        HashMap<Integer, Integer> expected = new HashMap<Integer, Integer>();
        int length = nums.length;
        
        for (int i = 0; i < length; i++){
            if (expected.containsKey(nums[i])){
                res[0] = expected.get(nums[i]) + 1;
                res[1] = i + 1;
                return res;
            }else{
                expected.put(target - nums[i],i);
            }
        }
    return res;
    }
}
```

#### O(n<sup>2</sup>) time, O(1) space
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] n = new int[2];
        for (int i = 0;i < nums.length; i++){
            for (int j = i + 1;j < nums.length; j++){
                if (target == (nums[i] + nums[j])){
                    n[0] = i+1;
                    n[1] = j+1;
                }
            }
        }
        return n;
    }
}
```
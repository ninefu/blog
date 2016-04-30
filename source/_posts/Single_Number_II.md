title: Single Number II
date: 2016-02-15 19:43:21
categories:
- Leetcode
tags:
- Leetcode
- Bit Manipulation
comments: true
---

Given an array of integers, every element appears three times except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

### HashMap O(n) time O(n) space solution


```java
public class Solution {
    public int singleNumber(int[] nums) {
        if (nums == null || nums.length < 1){return -1;}
        HashMap<Integer,Integer> counts = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++){
            if (counts.containsKey(nums[i])){
                int count = counts.get(nums[i]);
                if (count == 2){
                    counts.remove(nums[i]);
                }else{
                    counts.put(nums[i], count + 1);
                }
            }else{
                counts.put(nums[i], 1);
            }
        }
        
        Set<Map.Entry<Integer, Integer>> num = counts.entrySet();
        Iterator<Map.Entry<Integer, Integer>> it = num.iterator();
        Map.Entry<Integer, Integer> entry = it.next();
        return entry.getKey();
    }
}
```


### Bit solution

[Explanation](https://leetcode.com/discuss/31595/detailed-explanation-generalization-bitwise-operation-numbers)

```java
public class Solution {
    public int singleNumber(int[] nums) {
        int ones = 0, twos = 0;
        for (int i = 0; i < nums.length; i++){
            ones = (ones ^ nums[i]) & ~twos;
            twos = (twos ^ nums[i]) & ~ones;
        }
        return ones;
    }
}
```
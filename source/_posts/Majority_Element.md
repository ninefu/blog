title: Majority Element
date: 2016-01-11 17:02:20
categories:
- Leetcode
tags:
- Leetcode
- Divide and Conquer
- Array
- Bit
comments: true
---

Given an array of size n, find the majority element. The majority element is the element that appears more than ` n/2 ` times.

You may assume that the array is non-empty and the majority element always exist in the array.

<!--more-->

#### Sorting: O(n log n) time, O(1) space
```java
public class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}
```

#### Divide and Conquer: O(n log n) time, O(1) space

```java
public class Solution {
    public int majorityElement(int[] nums) {
        return majority(nums,0, nums.length - 1);
    }
    
    public int majority(int[] nums, int left, int right){
        if (left == right){return nums[left];}
        int mid = left + (right - left) / 2;
        int lm = majority(nums, left, mid);
        int rm = majority(nums, mid + 1, right);
        if (lm == rm){return lm;}
        return count(nums,left,right, lm) > count(nums,left, right, rm) ? lm: rm;
    }
    
    public int count(int[] nums, int left, int right, int num){
        int count = 0;
        for (int i = left; i <= right; i++){
            if (nums[i] == num){count++;}
        }
        return count;
    }
}
```

####  Hash Table: O(n) time, O(n) space

```java
public class Solution {
    public int majorityElement(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        int length = nums.length;
        for (int i = 0; i < length; i++){
            if (map.containsKey(nums[i])){
                map.put(nums[i], map.get(nums[i]) + 1);
            }else{
                map.put(nums[i], 1);
            }
            if (map.get(nums[i]) > length/2){
                return nums[i];
            }
        }
        return -1;
    }
}
```

#### Boyer-Moore Majority Vote Algorithm: O(n) time, O(1) space

[Algorithm source](http://www.cs.utexas.edu/~moore/best-ideas/mjrty/)

Another helpful [post](http://gregable.com/2013/10/majority-vote-algorithm-find-majority.html) about this algorithm.

> Basic idea of the algorithm is if we cancel out each occurrence of an element e with all the other elements that are different from e then e will exist till end if it is a majority element.

```java
public class Solution {
    public int majorityElement(int[] nums) {
        int cur = nums[0], count = 0;
        
        for (int i = 0; i < nums.length; i++){
            if (count == 0){
                cur = nums[i];
                count++;
            }else if (nums[i] == cur){
                count++;
            }else if (nums[i] != cur){
                count--;
            }
        }
        
        // can add a second O(n) pass to confirm that this number is
        // indeed the majority element by counting its frequency
        
        return cur;
    }
}
```

#### Randomization, 3ms

Adapted from Leetcode Discussion Board

```java
import java.util.Random;
public class Solution {
    public int majorityElement(int[] nums) {
        int length = nums.length;
        Random rd = new Random();
        while (true){
            int idx = rd.nextInt(length);
            int candidate = nums[idx];
            int count = 0;
            for (int i = 0; i < length; i++){
                if (nums[i] == candidate)
                    count++;
            }
            if (count > length / 2) {return candidate;}
        }
    }
}
```

#### Bit Manipulation

Cited from Leetcode Discussion Board

```java
public int majorityElement(int[] nums) {
    int[] bit = new int[32];
    for (int num: nums)
        for (int i=0; i<32; i++) 
            if ((num >> (31-i) & 1) == 1)
                bit[i]++;
    int ret=0;
    for (int i=0; i<32; i++) {
        bit[i]= bit[i]>nums.length/2 ? 1 : 0;
        ret += bit[i]*(1<<(31-i));
    }
    return ret;
}
```

or 

```java
public int majorityElement(int[] num) {
    int ret = 0;

    for (int i = 0; i < 32; i++) {
        int ones = 0, zeros = 0;
        for (int j = 0; j < num.length; j++) {
            if ((num[j] & (1 << i)) != 0) {
                ++ones;
            }
            else
                ++zeros;
        }
        if (ones > zeros)
            ret |= (1 << i);
    }

    return ret;
}
```

title: Two Sum II - Input array is sorted
date: 2016-02-21 15:22:34
categories:
- Leetcode
tags:
- Leetcode
- Array
- Two Pointers
- Binary Search
comments: true
---
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2


### Two pointers O(n) solution

```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] res = new int[2];
        if (numbers == null || numbers.length < 1)
            return res;
            
        int left = 0, right = numbers.length - 1;
        while(left < right){
            int sum = numbers[left] + numbers[right];
            if (sum == target){
                res[0] = left + 1;
                res[1] = right + 1;
                break;
            }else if (sum > target){
                right--;
            }else if (sum < target){
                left++;
            }
        }
        
        return res;
    }
}
```


### Binary Search O(n log n) solution

```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] res = new int[2];
        if (numbers == null || numbers.length < 1)
            return res;
            
        for (int i = 0; i < numbers.length; i++){
            if (numbers[i] + numbers[numbers.length - 1] < target)
                continue;
            int index = binarySearch(numbers, i, target - numbers[i]);
            if (index != -1){
                res[0] = i + 1;
                res[1] = index + 1;
                break;
            }
        }
        
        return res;
    }
    
    public int binarySearch(int[] numbers, int start, int target){
        int end = numbers.length;
        int mid = (start + end) / 2;
        
        while (start < mid && mid < end){
            int cur = numbers[mid];
            if (cur < target){
                start = mid;
            }else if (cur > target){
                end = mid;
            }else{
                return mid;
            }
            mid = (start + end) / 2;
        }
        return -1;
    }
}
```
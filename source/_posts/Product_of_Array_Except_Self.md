title: Product of Array Except Self
date: 2016-02-14 20:33:13
categories:
- Leetcode
tags:
- Leetcode
- Array
comments: true
---

Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].

Follow up:
Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

Mosted voted solution

```java
public class Solution {
	public int[] productExceptSelf(int[] nums) {
		int n = nums.length;
		int[] res = new int[n];
		res[0] = 1;
		for (int i = 1; i < n; i++) {
			res[i] = res[i - 1] * nums[i - 1];
		}
		int right = 1;
		for (int i = n - 1; i >= 0; i--) {
			res[i] *= right;
			right *= nums[i];
		}
		return res;
	}
}
```


> The product basically is calculated using the numbers before the current number and the numbers after the current number. Thus, we can scan the array twice. First, we calcuate the running product of the part before the current number. Second, we calculate the running product of the part after the current number through scanning from the end of the array.


```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null){return new int[0];}
        
        int length = nums.length;
        int[] res = new int[length];
        
        int runningPrefix = 1;
        for (int i = 0; i < length; i++){
            res[i] = runningPrefix;
            runningPrefix *= nums[i];
        }
        
        int runningSuffix = 1;
        for (int i = length - 1; i >= 0; i--){
            res[i] *= runningSuffix;
            runningSuffix *= nums[i];
        }
        
        return res;
    }
}
```
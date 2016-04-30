title: House Robber
date: 2016-02-14 20:53:44
categories:
- Leetcode
tags:
- Leetcode
- Dynamic Programming
comments: true
---

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### O(n<sup>2</sup>) space
```java
public int rob(int[] num) {
    int[][] dp = new int[num.length + 1][2];
    for (int i = 1; i <= num.length; i++) {
        dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]);
        dp[i][1] = num[i - 1] + dp[i - 1][0];
    }
    return Math.max(dp[num.length][0], dp[num.length][1]);
}
```

### O(n) space

```java
public class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length < 1) return 0;
        
        int[] res = new int[nums.length + 2];
        res[0] = res[1] = 0;
        
        for (int i = 2; i < res.length; i++){
            res[i] = Math.max(res[i - 1], (res[i - 2] + nums[i - 2]));
        }
        
        return res[res.length - 1];
    }
}
```

### O(1) space
```java
public class Solution {
    public int rob(int[] nums) {
        int prevNo = 0;
        int prevYes = 0;
        
        for (int n : nums){
            int temp = prevNo;
            prevNo = Math.max(prevNo, prevYes);
            prevYes = n + temp;
        }
        
        return Math.max(prevNo, prevYes);
    }
}
```
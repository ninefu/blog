title: Add Digits
date: 2016-01-02 13:39:09
categories:
- Leetcode
tags:
- Leetcode
- Math
comments: true
---
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

<!--more-->
```java
public class Solution {
    public int addDigits(int num) {
        while (num >= 10){
            int sum = 0;
            while (num > 0){
                sum += num % 10;
                num /= 10;
            }
            num = sum;
        }
        return num;
    }
}
```

#### Without any loop/recursion in O(1) runtime
See explanaton on [Wikipedia](https://en.wikipedia.org/wiki/Digital_root) or [discussion on Leetcode](https://leetcode.com/discuss/52122/accepted-time-space-line-solution-with-detail-explanations)

```java
public class Solution {
    public int addDigits(int num) {
        return 1 + (num - 1) % 9;
    }
}
```
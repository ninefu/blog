title: Number of 1 Bits
date: 2016-01-08 18:00:21
categories:
- Leetcode
tags:
- Leetcode
- Bit
comments: true
---

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

<!--more-->

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        
        while (n != 0){
            count = count + (n & 1);
            n = n >>> 1;
        }
        
        return count;
    }
}
```

Another solution which works faster. x & (x-1) helps to remove right most 1 for x (from Leetcode Discussion board).

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        
        while(n != 0){
            n = n & (n-1);
            count++;
        }
        return count;
    }
}
```
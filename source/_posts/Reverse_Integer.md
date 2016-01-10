title: Reverse Integer
date: 2016-01-06 10:05:51
categories:
- Leetcode
tags:
- Leetcode
- Math
comments: true
---
Reverse digits of an integer.

Example1: x = 123, return 321

Example2: x = -123, return -321

<!--more-->

My solution:

```java
public class Solution {
    public int reverse(int x) {
        long rev = 0;
        boolean neg = false;
        
        if (x < 0){
            neg = true;
            x = -x;
        }
        
        while (x > 0){
            rev = rev * 10 + x % 10;
            x /= 10;
        }
        
        if (rev > (long) Integer.MAX_VALUE){return 0;}
        if (neg){rev = -rev;}
        return (int) rev;
    }
}
```

Most two voted solution on Leetcode

```java
public class Solution {
    public int reverse(int x) {
        int rev = 0;
        
        while (x != 0){
            int newR = rev * 10 + x % 10;
            if ((newR - x % 10) / 10 != rev){return 0;}
            rev = newR;
            x /= 10;
        }
        
        return rev;
    }
}
```

```java
public class Solution {
	public int reverse(int x) {
        long rev= 0;
        while( x != 0){
            rev= rev*10 + x % 10;
            x= x/10;
            if( rev > Integer.MAX_VALUE || rev < Integer.MIN_VALUE)
                return 0;
        }
        return (int) rev;
    }
}
```
title: Palindrome Number
date: 2016-01-05 21:06:16
categories:
- Leetcode
tags:
- Leetcode
- Math
comments: true
---
Determine whether an integer is a palindrome. Do this without extra space.

<!--more-->
It turns out that there is no need to prevent overflow when reversing the integer. Palindrome of X will result in a negative number because of overflow, and that makes it never equals to the input number x

```java
public class Solution {
    public boolean isPalindrome(int x) {
        //if (x < 0 || x == Integer.MAX_VALUE){return false;}
        
        int old = x, cur = 0;
        
        while (x > 0){
            cur = cur * 10 + x % 10;
            x /= 10;
        }
        
        return old == cur;
    }
}
```

A solution that prevents overflow.

```java
public class Solution {
	public boolean isPalindrome(int x) {
        if( x < 0 || (x != 0 && x % 10 == 0)) return false;
        int sum=0;
        
        // half of the digits
        while(x > sum){
            sum = sum * 10 + x % 10;
            x/= 10;
        }
        // even || odd 
        return (x == sum) || (x == sum/10);
    }
}
```
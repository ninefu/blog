title: Power of Three
date: 2016-01-12 16:27:15
categories:
- Leetcode
tags:
- Leetcode
- Math
comments: true
---

Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?

<!--more-->

#### Iterative soltuion

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        while (n > 1){
            if (n % 3 != 0){
                return false;
            }else{
                n /= 3;
            }
        }
        return n == 1;
    }
}
```

#### Recursive solution
```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        return n > 0 && (n == 1 || (n % 3 == 0 && isPowerOfThree(n / 3)));
    }
}
```

#### Math solutions

Cited from Leetcode Discussion board


```java
// find the maximum power of 3 first
public class Solution {
    public boolean isPowerOfThree(int n) {
        int maxPower = (int) Math.pow(3, (int)(Math.log(0x7fffffff) / Math.log(3)));
        return n > 0 && maxPower % n == 0;
    }
}
```

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0 ){return false;}
        return (Math.log10(n) / Math.log10(3)) % 1 == 0;
    }
}
```

```java
public boolean isPowerOfThree(int n) {
    return n==0 ? false : n==Math.pow(3, Math.round(Math.log(n) / Math.log(3)));
}
```

```java
public boolean isPowerOfThree(int n) {
    int[] allPowerOfThree = new int[]{1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049, 177147, 531441, 1594323, 4782969, 14348907, 43046721, 129140163, 387420489, 1162261467};
    return Arrays.binarySearch(allPowerOfThree, n) >= 0;
}
```

#### Radix-3 Solution

cited from Leetcode Discussion board

>The idea is that the ternary number that is power of 3 will be something like 10,100,1000, etc, analogous to binary numbers that are powers of 2.

```java
public boolean isPowerOfThree(int n) {
    return Integer.toString(n, 3).matches("10*");
}
```
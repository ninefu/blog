title: Excel
date: 2016-01-11 16:23:47
categories:
- Leetcode
tags:
- Leetcode
- Math
---

Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

<!--more-->

For example:

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

```java
public class Solution {
    public int titleToNumber(String s) {
        if (s == null || s.length() < 1){return 0;}
        int col = 0;
        for (int i = 0; i < s.length(); i++){
            char cur = s.charAt(i);
            if (cur < 'A' || cur > 'Z'){return 0;}
            col = col * 26 + (int) (cur - 'A' + 1);
        }
        return col;
    }
}
```
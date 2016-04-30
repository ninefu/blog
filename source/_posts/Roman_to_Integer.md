title: Roman to Integer
date: 2016-01-26 17:04:08
categories:
- Leetcode
tags:
- Leetcode
- Math
- String
comments: true
---

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

```java
public class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() < 1){return 0;}
        int[] values = new int[26];
        values['I' - 'A'] = 1;
        values['V' - 'A'] = 5;
        values['X' - 'A'] = 10;
        values['L' - 'A'] = 50;
        values['C' - 'A'] = 100;
        values['D' - 'A'] = 500;
        values['M' - 'A'] = 1000;
        char[] chars = s.toCharArray();
        int res = 0, prev = 1000;
        for (char c : chars){
            int cur = values[c - 'A'];
            if (cur > prev){
                if (cur / prev > 10){return 0;}
                res -= 2 * prev;
            }
            res += cur;
            prev = cur;
        }
        return res;
    }
}
```

The first solution is much faster than using a HashMap


```java
public class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() < 1){return 0;}
        HashMap<Character, Integer> values = new HashMap<Character, Integer>();
        values.put('I',1);
        values.put('V',5);
        values.put('X',10);
        values.put('L',50);
        values.put('C',100);
        values.put('D',500);
        values.put('M',1000);
        char[] chars = s.toCharArray();
        int res = 0, prev = 1000;
        for (char c : chars){
            int cur = values.get(c);
            if (cur > prev){
                if (cur / prev > 10){return 0;}
                res -= 2 * prev;
            }
            res += cur;
            prev = cur;
        }
        return res;
    }
}
```
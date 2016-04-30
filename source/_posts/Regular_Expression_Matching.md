title: Regular Expression Matching
date: 2016-01-26 12:56:30
categories:
- Leetcode
tags:
- Leetcode
- Dynamic Programming
- Backtracking
- String
comments: true
---

Implement regular expression matching with support for '.' and '*'.

<!--more-->

'.' Matches any single character.

'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:

```
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

### DP solution 

```java
public class Solution {
	/**
	 * match[i][j]: if s[0...i-1] matches p[0...j-1]
	 * if p[j-1] != '*':
	 *     match[i][j] = match[i-1][j-1] && s[i-1] = p[j-1]
	 * if p[j-1] == '*', denote x = p[j-2]:
	 *     match[i][j] is true iff meets one of the following:
	 *         "x*" repeats 0 time and matches empty: match[i][j-2]
	 *         "x*" repeats >= 1 time and matches "x*x": s[i-1] == x && match[i-1][j]
	**/
    public boolean isMatch(String s, String p) {
        if (p == null){return s == null;}
        int pLength = p.length(), sLength = s.length();
        boolean[][] match = new boolean[sLength + 1][pLength + 1];
        
        //initialize
        match[0][0] = true;
        // the first for loop can be omited since boolean array 
        // is initialized to false
        for (int i = 1; i <= sLength; i++){
            match[i][0] = false; // always false between null and any non-null character
        }
        for (int j = 1; j <= pLength; j++){
            match[0][j] = (j > 1 && p.charAt(j - 1) == '*' && match[0][j - 2]); // "s" and "x*" return true
        }
        
        for (int i = 1; i <= sLength; i++){
            for (int j = 1; j <= pLength; j++){
                if (p.charAt(j - 1) != '*'){
                    match[i][j] = match[i - 1][j - 1] && charMatch(s.charAt(i - 1), p.charAt(j - 1));
                }else{
                    match[i][j] = match[i][j - 2] || (charMatch(s.charAt(i - 1), p.charAt(j - 2)) && match[i - 1][j]);
                }
            }
        }
        return match[sLength][pLength];
    }
    
    public boolean charMatch(char s, char p){
        return p == '.' || s == p;
    }
}
```

### Recursive solution

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if (p.isEmpty()){return s.isEmpty();}
        
        if (p.length() == 1 || p.charAt(1) != '*'){
            if (s.isEmpty() || !charMatch(s.charAt(0), p.charAt(0))){
                return false;
            }else{
                return isMatch(s.substring(1),p.substring(1));
            }
        }
        
        // p.length() > 1 && p.charAt(1) == '*'
        while(!s.isEmpty() && charMatch(s.charAt(0), p.charAt(0))){
            if (isMatch(s, p.substring(2))){return true;}
            s = s.substring(1);
        }
        
        return isMatch(s, p.substring(2));
    }
    
    public boolean charMatch(char s, char p){
        return p == '.' || p == s;
    }
}
```
title: Longest Palindromic String
date: 2016-01-03 11:33:57
categories:
- Leetcode
tags:
- Leetcode
- String
- Two Pointers
comments: true
---
Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

```java
public class Solution {
    public String longestPalindrome(String s) {
        if (s.length() < 2) return s;
        int start = 0, maxLength = 1;
        
        for (int i = 0; i < s.length();){
            if (s.length() - i <= maxLength / 2) break;
            int j = i, k = i;
            
            // skip duplicates
            while (k < s.length() - 1 && s.charAt(k + 1) == s.charAt(k)){k++;} 
            // reset i
            i = k + 1;
            // expand
            while (k < s.length() - 1 && j > 0 && s.charAt(k + 1) == s.charAt(j - 1)){
                k++;
                j--;
            }
            
            if (maxLength < k - j + 1){
                start = j;
                maxLength = k - j + 1;
            }
        }
        
        return s.substring(start, start + maxLength);
    }
}
```
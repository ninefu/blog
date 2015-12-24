title: Longest Substring Without Repeating Characters
date: 2015-12-24 11:36:36
categories:
- Leetcode
tags:
- Leetcode
- Hash
- TwoPointers
- String
---

Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

<!--more-->

#### O(n) time, O(n) space
```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int length = s.length();
        if (length == 0){return 0;}
        int max = 0;
        HashMap<Character,Integer> cache = new HashMap<Character, Integer>();
        for (int i = 0, j = 0; i < length; i++){
            if (cache.containsKey(s.charAt(i))){
            		// if the char has appeared before, move the left pointer to the right of the previous position
            		// compare with the current j value
                j = Math.max(j,cache.get(s.charAt(i)) + 1);
            }
            cache.put(s.charAt(i), i);
            max = Math.max(max, i - j + 1);
        }
        
        return max;
    }
}
```

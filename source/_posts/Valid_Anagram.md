title: Valid Anagram
date: 2016-01-10 19:21:51
categories: 
- Leetcode
tags:
- Leetcode
- Hash
- Sort
---
Given two strings s and t, write a function to determine if t is an anagram of s.

<!--more-->

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?

O(2n + 26)

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s == null || t == null || s.length() != t.length()){return false;}
        int[] counts = new int[26];
        
        for (int i = 0; i < s.length(); i++){
            counts[s.charAt(i) - 'a']++;
            counts[t.charAt(i) - 'a']--;
        }
        
        for (int j = 0; j < counts.length; j++){
            if (counts[j] != 0){
                return false;
            }
        }
        return true;
    }
}
```

#### HashMap solution for the follow up

O(2n)

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s == null || t == null || s.length() != t.length()) return false;
        
        HashMap<Character,Integer> map = new HashMap<Character, Integer>();
        
        for (int i = 0; i < s.length(); i++){
            char cur = s.charAt(i);
            if (map.containsKey(cur)){
                map.put(cur, map.get(cur) + 1);
            }else{
                map.put(cur, 1);
            }
        }
        
        for (int j = 0; j < t.length(); j++){
            char Cur = t.charAt(j);
            if (map.containsKey(Cur)){
                int count = map.get(Cur) - 1;
                if (count == 0){
                    map.remove(Cur);
                }else{
                    map.put(Cur, count);
                }
            }else{
                return false;
            }
        }
        
        return true;
    }
}
```
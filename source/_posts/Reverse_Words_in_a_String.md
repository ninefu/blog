title: Reverse Words in a String
date: 2016-01-31 11:23:13
categories:
- Leetcode
tags:
- Leetcode
- String
comments: true
---

Given an input string, reverse the string word by word.

For example,
Given s = "the sky is blue",
return "blue is sky the".

### Two pass solution

```java
public class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0){return "";}
        StringBuilder sb = new StringBuilder();
        String[] input = s.trim().split("\\s+");
        int length = input.length;
        
        if (input.length > 0){
            for (int i = length - 1; i > 0; i--){
                sb.append(input[i]);
                sb.append(" ");
            }
            sb.append(input[0]);
        }
        
        return sb.toString();
    }
}
```

### One pass solution

```java
public class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0){return "";}
        StringBuilder sb = new StringBuilder();
        int end = s.length();
        
        for (int i = s.length() - 1; i >= 0; i--){
            if (s.charAt(i) == ' '){
                if (end - i > 1){
                    sb.append(s.substring(i + 1, end));
                    sb.append(" ");
                }
                end = i;
            }else{
                if (i == 0){sb.append(s.substring(i, end));}
            }
        }
        
        return sb.toString().trim();
    }
}
```
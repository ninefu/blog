title: Longest Common Prefix
date: 2016-01-26 17:30:09
categories:
- Leetcode
tags:
- Leetcode
- String
comments: true
---

Write a function to find the longest common prefix string amongst an array of strings.

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        StringBuffer result = new StringBuffer();
        if (strs == null || strs.length < 1) return "";
        
        Arrays.sort(strs);
        char[] first = strs[0].toCharArray();
        char[] last = strs[strs.length - 1].toCharArray();
        
        for (int i = 0; i < first.length && i < last.length; i++){
            if (first[i] == last[i]){
                result.append(first[i]);
            }else{
                break;
            }
        }
        
        return result.toString();
    }
}
```


```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0)    return "";
        String pre = strs[0];
        int i = 1;
        while(i < strs.length){
            while(strs[i].indexOf(pre) != 0)
                pre = pre.substring(0,pre.length()-1);
            i++;
        }
        return pre;
    }
}
```

### brute force

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length < 1){return "";}
        
        String res = strs[0];
        for (int i = 1; i < strs.length; i++){
            res = common(res, strs[i]);
        }
        return res;
    }
    
    public String common(String s, String p){
        if (s == null || p == null){return "";}
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < s.length() && i < p.length(); i++){
            if (s.charAt(i) == p.charAt(i)){
                sb.append(s.charAt(i));
            }else{
                break;
            }
        }
        return sb.toString();
    }
}
```
title: Reverse Words in a String II
date: 2016-01-31 12:45:14
categories:
- Leetcode
tags:
- Leetcode
- String
comments: true
---

Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

For example,
Given s = "the sky is blue",
return "blue is sky the".

Could you do it in-place without allocating extra space?

```java
public class Solution {
    public void reverseWords(char[] s) {
        if (s == null || s.length == 0){return;}
        int length = s.length;
        // reverse the entire input
        reverse(s, 0, length - 1);
        // reverse each word
        int start = 0;
        for (int j = 0; j < length; j++){
            if (s[j] == ' '){
                reverse(s, start, j - 1);
                start = j + 1;
            }
        }
        // reverse the last word
        reverse(s, start, length - 1);
    }
    
    public void reverse(char[] s, int left, int right){
        if (s == null || s.length < 2 || left >= right){return;}
        while(left < right){
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```

or

```java
public class Solution{}
	public void reverseWords(char[] s){
        reverseWords(s,0,s.length-1);
        for(int i = 0, j = 0;i <= s.length;i++){
            if(i==s.length || s[i] == ' '){
                reverseWords(s,j,i-1);
                j = i+1;
            }
        }
    }

    private void reverseWords(char[] s, int begin, int end){
        while(begin < end){
            char c = s[begin];
            s[begin] = s[end];
            s[end] = c;
            begin++;
            end--;
        }
    }
}
```
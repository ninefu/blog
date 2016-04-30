title: Valid Palindrome
date: 2016-02-15 11:29:45
categories:
- Leetcode
tags:
- Leetcode
- String
- Two Pointers
comments: true
---
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

```java
public class Solution {
    public boolean isPalindrome(String s) {
        if (s == null){return false;}
        s = s.toLowerCase();
        int left = 0, right = s.length() - 1;
        char cLeft, cRight;
        
        while (left < right){
            cLeft = s.charAt(left);
            cRight = s.charAt(right);
            if (! Character.isLetterOrDigit(cLeft)){
                left++;
            }else if (! Character.isLetterOrDigit(cRight)){
                right--;
            }else{
                if (cLeft != cRight){
                    return false;
                }
                left++;
                right--;
            }
        }
        return true;
    }
}
```
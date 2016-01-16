title: Valid
date: 2016-01-11 16:53:00
categories:
- Leetcode
tags:
- Leetcode
- Stack
- String
comments: true
---

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

<!--more-->

```java
public class Solution {
    public boolean isValid(String s) {
        if (s == null || s.length() < 1 || s.length() % 2 == 1){return false;}
        Stack<Character> stack = new Stack<Character>();

        for (int i = 0; i < s.length(); i++){
            char cur = s.charAt(i);
            if (cur == '{' || cur == '[' || cur == '('){
                stack.push(cur);
            }else if (cur == '}' && !stack.empty() && stack.peek() == '{'){
                stack.pop();
            }else if (cur == ']' && !stack.empty() && stack.peek() == '['){
                stack.pop();
            }else if (cur == ')' && !stack.empty() && stack.peek() == '('){
                stack.pop();
            }else{
                return false;
            }
        }
        return stack.empty();
    }
}
```

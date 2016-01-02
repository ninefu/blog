title: Palindrome Permutation
date: 2016-01-02 12:37:46
categories:
- Leetcode
tags:
- Leetcode
- Hash
- String
---

Given a string, determine if a permutation of the string could form a palindrome.

For example,
"code" -> False, "aab" -> True, "carerac" -> True.

<!--more-->
One pass without counters.

```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        HashSet<Character> set = new HashSet<Character>();
        for (int i = 0; i < s.length(); i++){
            if (!set.add(s.charAt(i))){
                set.remove(s.charAt(i));
            }
        }
        
        return set.size() <= 1;
    }
}
```


Using a Bitset

```java
public boolean canPermutePalindrome(String s) {
    BitSet bs = new BitSet();
    for (byte b : s.getBytes())
        bs.flip(b);
    return bs.cardinality() < 2;
}
```
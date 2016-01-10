title: Shortest Word Distance
date: 2016-01-06 23:04:07
categories:
- Leetcode
tags:
- Leetcode
- Array
comment: true
---
Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

For example,
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

Given word1 = “coding”, word2 = “practice”, return 3.
Given word1 = "makes", word2 = "coding", return 1.

Note:
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

<!--more-->

```java
public class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
        int index = -1, dist = Integer.MAX_VALUE;
        
        for (int i = 0; i < words.length; i++){
            if (words[i].equals(word1) || words[i].equals(word2)){
                if (index != -1 && !words[index].equals(words[i])){
                    dist = Math.min(dist, i - index);
                }
                index = i;
            }
        }
        return dist == Integer.MAX_VALUE ? -1 : dist;
    }
}
```
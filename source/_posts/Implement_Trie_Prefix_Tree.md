title: Implement Trie (Prefix Tree)
date: 2016-02-23 19:04:32
categories:
- Leetcode
tags:
- Leetcode
- Trie
- Design
comments: true
---

Implement a trie with insert, search, and startsWith methods.

Note:
You may assume that all inputs are consist of lowercase letters a-z.

```java
class TrieNode {
    boolean isWord;
    TrieNode[] children;
    
    // Initialize your data structure here.
    public TrieNode() {
        children = new TrieNode[26];
        isWord = false;
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        if (word != null || word.length() > 0){
            TrieNode cur = root;
            for(int i = 0; i < word.length(); i++){
                int index = word.charAt(i) - 'a';
                if (cur.children[index] == null){
                    cur.children[index] = new TrieNode();
                }
                cur = cur.children[index];
            }
            cur.isWord = true;
        }
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
        if (word == null) return false;

        TrieNode cur = root;
        for(int i = 0; i < word.length(); i++){
            int index = word.charAt(i) - 'a';
            if (cur.children[index] == null)
                return false;
            cur = cur.children[index];
        }
        
        return cur.isWord;
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        if (prefix == null) return false;
        
        TrieNode cur = root;
        for(int i = 0; i < prefix.length(); i++){
            int index = prefix.charAt(i) - 'a';
            if (cur.children[index] == null)
                return false;
            cur = cur.children[index];
        }
        return true;
    }
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```
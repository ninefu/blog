title: Add and Search Word - Data structure design
date: 2016-02-23 19:59:25
categories:
- Leetcode
tags:
- Leetcode
- Backtracking
- Trie
- Design
comments: true
---
Design a data structure that supports the following two operations:

void addWord(word)
bool search(word)
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

For example:

addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
Note:
You may assume that all words are consist of lowercase letters a-z.


### Solution using Trie

```java
public class WordDictionary {
    TrieNode root = new TrieNode();
    
    private class TrieNode{
        public boolean isWord;
        public TrieNode[] children;
        
        public TrieNode(){
            isWord = false;
            children = new TrieNode[26];
        }
    }

    // Adds a word into the data structure.
    public void addWord(String word) {
        if (word != null){
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

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        if (word == null) return false;
        return searchArray(word.toCharArray(), 0, root);
    }
    
    public boolean searchArray(char[] chars, int start, TrieNode node){
        TrieNode cur = node;
        for (int i = start; i < chars.length; i++){
            if (cur == null){
                break;
            }else{
                if (chars[i] != '.'){
                    int index = chars[i] - 'a';
                    cur = cur.children[index];
                }else{
                    TrieNode temp = cur;
                    for (int j = 0; j < 26; j++){
                        cur = temp.children[j];
                        if (searchArray(chars, i+1, cur))
                            return true;
                    }
                    return false;
                }
            }
        }
        return cur != null && cur.isWord;
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```


### Solution using Map

from [this post](https://leetcode.com/discuss/44509/java-solution-easy-understand)


```java
public class WordDictionary {

    Map<Integer, List<String>> map = new HashMap<Integer, List<String>>();
    // Adds a word into the data structure.
    public void addWord(String word) {
        int index = word.length();
        if(!map.containsKey(index)){
            List<String> list = new ArrayList<String>();
            list.add(word);
            map.put(index, list);
        }else{
            map.get(index).add(word);
        }

    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        int index = word.length();
        if(!map.containsKey(index)){
            return false;
        }
        List<String> list = map.get(index);
        if(isWords(word)){
            return list.contains(word);
        }
        for(String s : list){
            if(isSame(s, word)){
                return true;
            }
        }
        return false;
    }

    boolean isWords(String s){
        for(int i = 0; i < s.length(); i++){
            if(!Character.isLetter(s.charAt(i))){
                return false;
            }
        }
        return true;
    }

    boolean isSame(String a, String search){
        if(a.length() != search.length()){
            return false;
        }
        for(int i = 0; i < a.length(); i++){
            if(search.charAt(i) != '.' && search.charAt(i) != a.charAt(i)){
                return false;
            }
        }
        return true;
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```
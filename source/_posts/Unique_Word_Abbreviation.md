title: Unique Word Abbreviation
date: 2016-01-11 16:12:19
categories: 
- Leetcode
tags:
- Leetcode
- Hash
- Design
comments: true

---

An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:

<!--more-->

```
a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
```

Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

Example: 

```
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> false
isUnique("cart") -> true
isUnique("cane") -> false
isUnique("make") -> true
```

```java
public class ValidWordAbbr {
    HashMap<String,String> map = new HashMap<String, String>();
    
    public ValidWordAbbr(String[] dictionary) {
        for (String s : dictionary){
            String abbr = getAbbr(s);
            if (map.containsKey(abbr)){
                if (!map.get(abbr).equals(s)){
                    map.put(abbr,"");
                }
            }else{
                map.put(abbr,s);
            }
        }
    }

    public boolean isUnique(String word) {
        String abbr = getAbbr(word);
        return !map.containsKey(abbr) || map.get(abbr).equals(word);
    }
    
    public String getAbbr(String s){
        if (s == null || s.length() < 3){return s;}
        Integer length = s.length() - 2;
        return s.substring(0,1) + length.toString() + s.substring(s.length() - 1);
    }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```
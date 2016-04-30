title: ZigZag Conversion
date: 2016-01-21 11:27:25
categories:
- Leetcode
tags:
- Leetcode
- String
comments: true
---

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

<!--more-->

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```

`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

### My solution

```java
public class Solution {
    public String convert(String s, int numRows) {
        if (s == null || s.length() < 2 || numRows < 2){return s;}
        int numCols = (s.length() / (numRows + numRows - 2) + 1) * (1 + numRows - 2);

        char[][] grids = new char[numRows][numCols];
        for (int i = 0; i < s.length(); i++){
            int row = i % (numRows + numRows - 2);
            int col = i / (numRows + numRows - 2) * (1 + numRows - 2);
            if (row >= numRows){
                col += row % (numRows - 1);
                row = (numRows - 1 - row) + numRows - 1;
            }
            grids[row][col] = s.charAt(i);
        }

        StringBuffer res = new StringBuffer();
        for (int i = 0; i < grids.length; i++){
            for (int j = 0; j < grids[0].length; j++){
                if (grids[i][j] != '\u0000'){res.append(grids[i][j]);}
            }
        }
        
        return res.toString();
    }
}
```

### Most voted and much faster [solution](https://leetcode.com/discuss/10493/easy-to-understand-java-solution) on Leetcode

```java
public class Solution {
    public String convert(String s, int numRows) {
        if (s == null || s.length() < 1) return s;
        char[] letter = s.toCharArray();
        int length = letter.length;
        StringBuffer[] sb = new StringBuffer[numRows];
        for (int i = 0; i < sb.length; i++){
            sb[i] = new StringBuffer();
        }
        
        int i = 0;
        while (i < length){
            for (int pos = 0; pos < numRows && i < length; pos++){
                sb[pos].append(letter[i++]);
            }
            for(int pos = numRows - 2; pos > 0 && i < length; pos--){
                sb[pos].append(letter[i++]);
            }
        }
        
        for (int j = 1; j < numRows; j++){
            sb[0].append(sb[j]);
        }
        return sb[0].toString();
    }
}
```
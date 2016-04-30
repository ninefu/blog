title: Rectangle Area
date: 2016-02-10 15:45:02
categories:
- Leetcode
tags:
- Leetcode
- Math
comments: true


---

Find the total area covered by two rectilinear rectangles in a 2D plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

Assume that the total area is never beyond the maximum possible value of int.

```java
public class Solution {
    int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int left = Math.max(A,E), right = Math.max(min(C,G), left);
        int bottom = Math.max(B,F), top = Math.max(min(D,H), bottom);
        return (C-A)*(D-B) - (right-left)*(top-bottom) + (G-E)*(H-F);
    }
}
```
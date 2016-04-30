title: Flatten 2D Vector
date: 2016-01-30 20:19:26
categories:
- Leetcode
tags:
- Leetcode
- Design
comments: true
---

Implement an iterator to flatten a 2d vector.

For example,
Given 2d vector =

```
[
  [1,2],
  [3],
  [4,5,6]
]
```

By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: `[1,2,3,4,5,6]`.

```java
public class Vector2D {
    private Iterator<List<Integer>> it;
    private Iterator<Integer> j;
    
    public Vector2D(List<List<Integer>> vec2d) {
        it = vec2d.iterator();
    }

    public int next() {
        hasNext();
        return j.next();
    }

    public boolean hasNext() {
        while ((j == null || !j.hasNext()) && it.hasNext()){
            j = it.next().iterator();
        }
        return j != null && j.hasNext();
    }
}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
 ```
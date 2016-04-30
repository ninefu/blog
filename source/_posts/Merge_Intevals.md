title: Merge Intevals
date: 2016-02-15 21:49:29
categories:
- Leetcode
tags:
- Leetcode
- Arrays
- Sort
---

Given a collection of intervals, merge all overlapping intervals.

For example,

```
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
```

### O(n log n) solution

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() < 2){
            return intervals;
        }
        
        Collections.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval i1, Interval i2){
                return i1.start - i2.start;
            }
        });
        
        List<Interval> result = new LinkedList<Interval>();
        Interval prev = null;
        
        for (Interval interval : intervals){
            if (prev == null || prev.end < interval.start){
                result.add(interval);
                prev = interval;
            }else{
                prev.end = Math.max(prev.end, interval.end);
            }
        }
        
        return result;
    }
}
```
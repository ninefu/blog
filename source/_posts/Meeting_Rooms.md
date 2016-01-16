title: Meeting Rooms
date: 2016-01-10 19:53:58
categories: 
- Leetcode
tags:
- Leetcode
- Sort
---

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

<!--more-->

For example,
Given [[0, 30],[5, 10],[15, 20]],
return false.

O(nlogn).

```java
public class Solution {
    public boolean canAttendMeetings(Interval[] intervals) {
        if (intervals == null){return false;}
        
        Arrays.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval a, Interval b){
                return a.start - b.start;
            }
        });
        
        for (int i = 0; i < intervals.length - 1; i++){
            if (intervals[i + 1].start < intervals[i].end){
                return false;
            }
        }
        
        return true;
    }
}
```


The following two solutions are cited from Leetcode Discussion board.

####Find an overlap while sorting.

```java
private boolean canAttendMeetings(Interval[] intervals) {
    try {
        Arrays.sort(intervals, new IntervalComparator());
    } catch (Exception e) {
        return false;
    }
    return true;
}

private class IntervalComparator implements Comparator<Interval> {
    @Override
    public int compare(Interval o1, Interval o2) {
        if (o1.start < o2.start && o1.end <= o2.start)
            return -1;
        else if (o1.start > o2.start && o1.start >= o2.end)
            return 1;
        throw new RuntimeException();
    }
}
```

####Use lambda function in Java 8

```java
public boolean canAttendMeetings(Interval[] intervals) {
    // Sort the intervals by start time
    Arrays.sort(intervals, (x, y) -> x.start - y.start);
    for (int i = 1; i < intervals.length; i++)
        if (intervals[i-1].end > intervals[i].start)
            return false;
    return true;
}
```
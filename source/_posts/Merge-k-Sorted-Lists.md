title: Merge k Sorted Lists
date: 2016-03-03 19:07:00
categories:
- Leetcode
tags:
- Leetcode
- Divide and Conquer
- Linked List
- Heap
comments: true
---
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

### Heap, O(n log k) time complexity

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0)
            return null;
            
        PriorityQueue<ListNode> pq = new PriorityQueue<ListNode>(lists.length, new Comparator<ListNode>(){
            @Override
            public int compare(ListNode l1, ListNode l2){
                return l1.val - l2.val;
            }
        });
        
        for (int i = 0; i < lists.length; i++){
            if (lists[i] != null)
                pq.add(lists[i]);
        }
        
        ListNode prev = new ListNode(0);
        ListNode head = prev;
        
        while(pq.size() > 0){
            head.next = pq.poll();
            head = head.next;
            
            if (head.next != null){
                pq.add(head.next);
            }
        }
        return prev.next;
    }
}
```


### Recursion, divide and conquer

```java
public class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0)
            return null;
        
        return partition(lists, 0, lists.length - 1);
    }
    
    public ListNode partition(ListNode[] lists, int start, int end){
        if (start == end)
            return lists[start];
        
        if (start < end){
            int mid = (start + end) / 2;
            ListNode l1 = partition(lists, start, mid);
            ListNode l2 = partition(lists, mid + 1, end);
            return merge(l1, l2);
        }else{
            return null;
        }
    }
    
    public ListNode merge(ListNode l1, ListNode l2){
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val < l2.val){
            l1.next = merge(l1.next, l2);
            return l1;
        }else{
            l2.next = merge(l1,l2.next);
            return l2;
        }
    }
}
```
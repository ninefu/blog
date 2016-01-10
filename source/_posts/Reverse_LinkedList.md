title: Reverse Linked List
date: 2016-01-06 11:34:49
categories:
- Leetcode
tags:
- Leetcode
- LinkedList
comments: true
---

Reverse a singly linked list.

<!--more-->

Iterative

```java
public class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode newHead = null;
        
        while (head != null){
            ListNode next = head.next;
            head.next = newHead;
            newHead = head;
            head = next;
        }
        
        return newHead;
    }
}
```

Recursive

```java
public ListNode reverseList(ListNode head) {
    return reverseListInt(head, null);
}

public ListNode reverseListInt(ListNode head, ListNode newHead) {
    if(head == null)
        return newHead;
    ListNode next = head.next;
    head.next = newHead;
    return reverseListInt(next, head);
}
```
title: Remove Linked List Elements
date: 2016-01-06 15:34:43
categories:
- Leetcode
tags:
- Leetcode
- Linked List
comments: true
---

Remove all elements from a linked list of integers that have value val.

Example
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5

<!--more-->

#### Iterative solution with dummy

```java
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null){return null;}
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        
        while (head != null){
            if (head.val == val){
                prev.next = head.next;
            }else{
                prev = head;
            }
            head = head.next;

        }
        return dummy.next;
    }
}
```

#### Iterative solution without dummy

```java
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        while (head != null && head.val == val) head = head.next;
        ListNode curr = head;
        while (curr != null && curr.next != null)
            if (curr.next.val == val) curr.next = curr.next.next;
            else curr = curr.next;
        return head;
    }
}
```

#### Recursive solution
```java
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null){return null;}
        head.next = removeElements(head.next, val);
        return head.val == val? head.next : head;
    }
}
```
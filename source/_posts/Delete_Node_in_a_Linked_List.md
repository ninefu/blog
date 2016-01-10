title: Delete Node in a Linked List
date: 2016-01-06 15:23:00
categories: 
- Leetcode
tags:
- Leetcode
- LinkedList
comments: true
---
Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.

<!--more-->

```java
public class Solution {
    public void deleteNode(ListNode node) {
        if (node == null){return;}
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```
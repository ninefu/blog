title: Linked List Cycle
date: 2016-02-16 21:49:22
categories:
- Leetcode
tags:
- Linked List
- Two Pointers
comments: true
---

Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

O(n) time O(1) space

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null) return false;
        ListNode slower = head, faster = head;
        
        while (faster != null && faster.next != null){
            slower = slower.next;
            faster = faster.next.next;
            if (slower == faster){
                return true;
            }
        }
        
        return false;
    }
}
```
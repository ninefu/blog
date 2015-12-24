title: Add Two Numbers
date: 2015-12-24 11:05:43
categories:
- Leetcode
tags:
- Leetcode
- LinkedList
- Math
comments: true
---
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

<!--more-->
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int sum = 0;
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        
        while (l1 != null || l2 != null || sum != 0){
            if (l1 != null){
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null){
                sum += l2.val;
                l2 = l2.next;
            }
            ListNode next = new ListNode((sum) % 10);
            head.next = next;
            head = head.next;
            sum /= 10 ;
        }
        
        return dummy.next;
    }
}
```
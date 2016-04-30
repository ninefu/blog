title: Closest Binary Search Tree Value
date: 2016-02-21 15:21:25
categories:
- Leetcode
tags:
- Leetcode
- Tree
- Binary Search
comments: true
---

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Note:
Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.

### Recursive

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int closestValue(TreeNode root, double target) {
        int cur = root.val;
        TreeNode child = target < cur ? root.left : root.right;
        if (child == null) return cur;
        int next = closestValue(child, target);
        return Math.abs(target - cur) < Math.abs(target - next) ? cur : next;
        
    }
}
```


### Iterative

```java
public class Solution {
    public int closestValue(TreeNode root, double target) {
        int res = root.val;
        while (root != null){
            if (Math.abs(res - target) >= Math.abs(root.val - target))
                res = root.val;
            root = target < root.val ? root.left : root.right;
        }
        return res;
    }
}
```
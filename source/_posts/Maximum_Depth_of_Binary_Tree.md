title: Maximum Depth of Binary Tree
date: 2016-01-03 21:42:11
categories:
- Leetcode
tags:
- Leetcode
- Tree
- DFS
comments: true
---

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

<!--more-->

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
    public int maxDepth(TreeNode root) {
        return root != null ? (1 + Math.max(maxDepth(root.left), maxDepth(root.right))) : 0;
    }
}
```
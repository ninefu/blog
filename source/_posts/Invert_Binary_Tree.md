title: Invert Binary Tree
date: 2016-01-09 19:36:46
categories: Leetcode
tags:
- Leetcode
- Tree
comments: true
---
Invert a binary tree.

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
to

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

<!--more-->

####Recursive solution

```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null){return null;}
        
        TreeNode left = root.left;
        TreeNode right = root.right;
        root.left = invertTree(right);
        root.right = invertTree(left);
        return root;
    }
}
```

####Iterative Solution

```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null){return null;}
        
        // BFS/level order traversal if using a queue, DFS if using a stack
        Queue<TreeNode> queue = new LinkedList<TreeNode>(); 
        
        queue.add(root);
        
        while(queue.peek() != null){
            TreeNode cur = queue.poll();
            TreeNode temp = cur.left;
            cur.left = cur.right;
            cur.right = temp;
            if (cur.left != null){
                queue.add(cur.left);
            }
            if (cur.right != null){
                queue.add(cur.right);
            }
        }
        
        return root;
    }
}
```

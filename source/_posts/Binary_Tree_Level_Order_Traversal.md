title: Binary Tree Level Order Traversal
date: 2016-02-15 16:17:29
categories:
- Leetcode
tags:
- Leetcode
- Tree
- BFS
comments: true
---
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree {3,9,20,#,#,15,7},

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

### Using a queue to keep nodes in the same level

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>(); // result list
        List<Integer> sub; // sub list for each level
        if (root == null){return res;}
        
        Queue<TreeNode> level = new LinkedList<>();
        level.add(root);
        
        while (level.size() > 0){
            sub = new ArrayList<>();
            int levelNum = level.size();
            
            for (int i = 0; i < levelNum; i++){
                TreeNode cur = level.poll();
                if (cur.left != null) level.add(cur.left);
                if (cur.right != null) level.add(cur.right);
                sub.add(cur.val);
            }
            res.add(sub);
        }
        return res;
    }
}
```
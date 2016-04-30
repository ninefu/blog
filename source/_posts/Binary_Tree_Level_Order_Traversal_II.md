title: Binary Tree Level Order Traversal II
date: 2016-02-15 16:52:57
categories:
- Leetcode
tags:
- Leetcode
- Tree
- BFS
comments: true
---

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:

```
Given binary tree {3,9,20,#,#,15,7},
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:

```
[
  [15,7],
  [9,20],
  [3]
]
```


### BFS

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>(); // result list
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
            // insert at the beginning of the linkedlist
            res.add(0,sub);
        }
        return res;
    }
}
```


### DFS

> The attached is my current recursive solution. In each function call, we pass in the current node and its level. If this level does not yet exist in the output container, then we should add a new empty level. Then, we add the current node to the end of the current level, and recursively call the function passing the two children of the current node at the next level. This algorithm is really a DFS, but it saves the level information for each node and produces the same result as BFS would.
 
from this [post](https://leetcode.com/discuss/5353/there-better-regular-level-order-traversal-reverse-result)

```java
public class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        levelMaker(res, root, 0);
        return res;
    }
    
    public void levelMaker(List<List<Integer>> list, TreeNode root, int level){
        if (root == null) return;
        if (level >= list.size()){
            list.add(0, new LinkedList<Integer>());
        }
        levelMaker(list, root.left, level + 1);
        levelMaker(list, root.right, level + 1);
        list.get(list.size() - level - 1).add(root.val);
    }
}
```
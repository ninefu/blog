title: Lowest Common Ancestor of a Binary Tree
date: 2016-02-15 15:15:32
categories:
- Leetcode
tags:
- Leetcode
- Tree
comments: true
---

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

```
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
```

For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

### Recursive solution, O(n)

Since this is a binary tree not a binary search tree, if two nodes p and q are both on the same subtree (left or right), then the lowest common ancestor must be the node between q and p with higher hierachy in the tree. Otherwise, root is the lowest common ancestor. 

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        return left == null ? right : right == null ? left : root;
    }
}
```


### Iterative solution, O(2n)

```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Map<TreeNode, TreeNode> parent = new HashMap<>();
        Stack<TreeNode> stack = new Stack<>();
        parent.put(root,null);
        stack.push(root);
        
        // find the parent of all nodes
        while (!parent.containsKey(q) || !parent.containsKey(p)){
            TreeNode node = stack.pop();
            if (node.left != null){
                parent.put(node.left, node);
                stack.push(node.left);
            }
            if (node.right != null){
                parent.put(node.right, node);
                stack.push(node.right);
            }
        }
        
        // get the ancestor list starting from p
        Set<TreeNode> ancestors = new HashSet<>();
        while (p != null){
            ancestors.add(p);
            p = parent.get(p);
        }
        // go through q's ancestor list until find one the same as p
        while (! ancestors.contains(q)){
            q = parent.get(q);
        }
        return q;
    }
}
```


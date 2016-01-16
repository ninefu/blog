title: Same Tree
date: 2016-01-09 22:51:34
categories:
- Leetcode
tags:
- Leetcode
- Tree
- DFS
comments: true
---

Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

<!--more-->
#### Recursive solution

```java
public class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null || q == null) return p == q;
        return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

#### Iterative solution

From Leetcode Discussion board

```java
public class Solution {
	public boolean isSameTree(TreeNode p, TreeNode q) {
		Stack<TreeNode> stack_p = new Stack <> ();       
		Stack<TreeNode> stack_q = new Stack <> ();
		if (p != null) stack_p.push( p ) ;
		if (q != null) stack_q.push( q ) ;
		while (!stack_p.isEmpty() && !stack_q.isEmpty()) {
			TreeNode pn = stack_p.pop() ;
			TreeNode qn = stack_q.pop() ;          
			if (pn.val != qn.val) return false ;
			if (pn.right != null) stack_p.push(pn.right) ;
			if (qn.right != null) stack_q.push(qn.right) ;
			if (stack_p.size() != stack_q.size()) return false ;
			if (pn.left != null) stack_p.push(pn.left) ;                        
			if (qn.left != null) stack_q.push(qn.left) ;
			if (stack_p.size() != stack_q.size()) return false ;
		}           
		return stack_p.size() == stack_q.size() ;   
	}
}
````
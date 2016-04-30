title: Max Root to Leaf Sum
date: 2016-03-06 22:17:25
categories: 
- Interview
tags: 
- Technical Interview
- Tree
- DFS
comments: true
---

Find out the maximum cost of all the possible root-to-leaf paths

```java
public class solution{
	public int maxPathCost(Node root){
		if (root == null)
			return 0;
		if (root.left == null && root.right == null)
			return root.value;
		
		int leftMax = maxPathCost(root.left);
		int rightMax = maxPathCost(root.right);
		return root.val + leftMax > rightMax ? leftMax : rightMax;
	}
}
```
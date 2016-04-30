title: Remove Duplicates from Sorted Array II
date: 2016-01-20 18:02:13
categories:
- Leetcode
tags:
- Leetcode
- Array
- Two Pointers
comments: true
---

Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

<!--more-->

For example,
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null){return 0;}
        int index = 0;
        
        for (int num : nums){
            if (index < 2 || num > nums[index - 2]){
                nums[index++] = num;
            }
        }
        
        return index;
    }
}
```

### Extension to all duplicates at most K times

From Leetcode [post](https://leetcode.com/discuss/22584/share-time-and-solution-when-duplicates-allowed-most-times)

```java
int removeDuplicates(int A[], int n, int k) {
	if (n <= k) return n;
	int i = 1, j = 1;
	int cnt = 1;

	while (j < n) {
		if (A[j] != A[j-1]) {
			cnt = 1;
			A[i++] = A[j];
		}
		else {
			if (cnt < k) {
			A[i++] = A[j];
			cnt++;
			}
		}
		++j;
	}
return i;
}
```
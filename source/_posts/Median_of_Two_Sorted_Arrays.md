title: Median of Two Sorted Arrays
date: 2016-01-01 13:38:41
categories:
- Leetcode
tags:
- Leetcode
- Divide and Conquer
- Array
- Binary Search
comments: true
---
There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

<!--more-->
Compare the median of nums1 and nums2. If nums1's median is smaller than nums2's median, then compare the right half of nums1 and the left half of nums2 for the next iteration, or vice versa. Do this recursively until k = 1.


Time complexity O(log(m+n))

```java
public class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length, n = nums2.length;
        int l = (m + n + 1)/2, r = (m + n + 2)/2;
        return (getKth(nums1,0,nums2,0,l) + getKth(nums1,0,nums2,0,r))/2.0;
    }
    
    public double getKth(int[] a, int aStart, int[] b, int bStart, int k){
        if (aStart > a.length - 1){return b[bStart + k - 1];}
        if (bStart > b.length - 1){return a[aStart + k - 1];}
        if (k == 1){return Math.min(a[aStart],b[bStart]);}
        
        int aMid = Integer.MAX_VALUE, bMid = Integer.MAX_VALUE;
        if ((aStart + k/2 - 1) < a.length) aMid = a[aStart + k/2 - 1];
        if ((bStart + k/2 - 1) < b.length) bMid = b[bStart + k/2 - 1];
        
        if (aMid < bMid){
            return getKth(a, aStart + k/2, b, bStart, k-k/2);
        }else{
            return getKth(a, aStart, b, bStart + k/2, k-k/2);
        }
    }
}
```

Or an O(log(min(m,n))) iterative solution ([explanation](https://leetcode.com/discuss/41621/very-concise-iterative-solution-with-detailed-explanation))

```java
 double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    int N1 = nums1.size();
    int N2 = nums2.size();
    if (N1 < N2) return findMedianSortedArrays(nums2, nums1);   // Make sure A2 is the shorter one.

    if (N2 == 0) return ((double)nums1[(N1-1)/2] + (double)nums1[N1/2])/2;  // If A2 is empty

    int lo = 0, hi = N2 * 2;
    while (lo <= hi) {
        int mid2 = (lo + hi) / 2;   // Try Cut 2 
        int mid1 = N1 + N2 - mid2;  // Calculate Cut 1 accordingly

        double L1 = (mid1 == 0) ? INT_MIN : nums1[(mid1-1)/2];  // Get L1, R1, L2, R2 respectively
        double L2 = (mid2 == 0) ? INT_MIN : nums2[(mid2-1)/2];
        double R1 = (mid1 == N1 * 2) ? INT_MAX : nums1[(mid1)/2];
        double R2 = (mid2 == N2 * 2) ? INT_MAX : nums2[(mid2)/2];

        if (L1 > R2) lo = mid2 + 1;     // A1's lower half is too big; need to move C1 left (C2 right)
        else if (L2 > R1) hi = mid2 - 1;    // A2's lower half too big; need to move C2 left.
        else return (max(L1,L2) + min(R1, R2)) / 2; // Otherwise, that's the right cut.
    }
    return -1;
} 
```
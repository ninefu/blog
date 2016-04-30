title: Candy
date: 2016-02-24 20:11:35
categories:
- Leetcode
tags:
- Leetcode
- Greedy
comments: true
---
There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
What is the minimum candies you must give?


```java
public class Solution {
    public int candy(int[] ratings) {
        if (ratings == null)return 0;
        int length = ratings.length;
        if (length <= 1) return length;
        int[] candies = new int[length];

        for(int i = 0; i < length; i++){
            if (i > 0 && ratings[i] > ratings[i - 1]){
                candies[i] = candies[i - 1] + 1;
            }else{
                candies[i] = 1;
            }
        }
        int result = 0;
        for(int j = ratings.length - 1; j >= 0; j--){
            if (j >0 && ratings[j] < ratings[j - 1]){
                candies[j - 1] = Math.max(candies[j] + 1, candies[j - 1]);
            }
            result += candies[j];
        }
        return result;
    }
}
```


[Another solution from Leetcode](https://leetcode.com/discuss/23835/one-pass-constant-space-java-solution)

```java
public class Solution {
    public int candy(int[] ratings) {
        if (ratings == null || ratings.length == 0) return 0;
        int total = 1, prev = 1, countDown = 0;
        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i] >= ratings[i-1]) {
                if (countDown > 0) {
                    total += countDown*(countDown+1)/2; // arithmetic progression
                    if (countDown >= prev) total += countDown - prev + 1;
                    countDown = 0;
                    prev = 1;
                }
                prev = ratings[i] == ratings[i-1] ? 1 : prev+1;
                total += prev;
            } else countDown++;
        }
        if (countDown > 0) { // if we were descending at the end
            total += countDown*(countDown+1)/2;
            if (countDown >= prev) total += countDown - prev + 1;
        }
        return total;
    }
}
```
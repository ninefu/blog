title: Paint House I & II
date: 2016-01-30 15:45:37
categories:
- Leetcode
tags:
- Leetcode
- Dynamic Programming
comments: true
---
## Paint House I

There are a row of n houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a n x 3 cost matrix. For example, costs[0][0] is the cost of painting house 0 with color red; costs[1][2] is the cost of painting house 1 with color green, and so on... Find the minimum cost to paint all houses.

Note:
All costs are positive integers.

O(n) time and O(1) space

```java
public class Solution {
    public int minCost(int[][] costs) {
        if (costs == null || costs.length < 1){
            return 0;
        }
        
        for (int i = 1; i < costs.length; i++){
            costs[i][0] += Math.min(costs[i - 1][1], costs[i - 1][2]);
            costs[i][1] += Math.min(costs[i - 1][0], costs[i - 1][2]);
            costs[i][2] += Math.min(costs[i - 1][0], costs[i - 1][1]);
        }
        
        int n = costs.length - 1;
        return Math.min(costs[n][0], Math.min(costs[n][1],costs[n][2]));
    }
}
```


```java
// starting from the second house/row, costs[i][0] represents the cost of painting this house red plus the previous house, etc
public class Solution {
    public int minCost(int[][] costs) {
        if (costs == null || costs.length < 1){
            return 0;
        }
        int length = costs.length, r = 0, b = 0, g = 0;
        
        for (int i = 0; i < length; i++){
            int rr = r, bb = b, gg = g;
            r = costs[i][0] + Math.min(bb, gg);
            g = costs[i][1] + Math.min(rr, bb);
            b = costs[i][2] + Math.min(rr, gg);
        }
        
        return Math.min(r, Math.min(g, b));
    }
}
```

## Paint House II

The cost of painting each house with a certain color is represented by a n x k cost matrix. For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses. Could you solve it in O(nk) runtime?

### O（nk<sup>2</sup>）solution

```java
public class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length < 1){
            return 0;
        }
        int length = costs.length, numColor = costs[0].length;
        
        int[][] totalCosts = new int[length + 1][numColor];
        for (int j = 0; j < numColor; j++){
            totalCosts[0][j] = 0;
        }
        for (int i = 1; i < length + 1; i++){
            for (int m = 0; m < numColor; m++){
                // costs of paint the ith house with color m + the previous house
                int prevMin = getMin(totalCosts, numColor, i - 1, m);
                totalCosts[i][m] = costs[i - 1][m] + prevMin;
            }
        }
        
        return getMin(totalCosts, numColor, length, numColor + 1);
    }
    
    public int getMin(int[][] totalCosts, int numColor, int prevHouse, int currentColor){
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < numColor; i++){
            if (i == currentColor && i == 0 && numColor - 1 == currentColor){
                return 0;
            }else if (i == currentColor){
                continue;
            }else{
                min = Math.min(totalCosts[prevHouse][i], min);
            }
        }
        return min;
    }
}
```

### O(nk) solution

```java
public class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length == 0){return 0;}
        
        int n = costs.length, k = costs[0].length;
        int min1 = -1, min2 = -1;
        
        for (int i = 0; i < n; i++){
            int last1 = min1, last2 = min2;
            min1 = -1; min2 = -1;
            
            for (int j = 0; j < k; j++){
                if (j != last1){
                    //current color j is different to last min1
                    costs[i][j] += last1 < 0 ? 0 : costs[i - 1][last1];
                }else{
                    costs[i][j] += last2 < 0 ? 0 : costs[i - 1][last2];
                }
                
                //update min value index
                if (min1 < 0 || costs[i][j] < costs[i][min1]){
                    min2 = min1;
                    min1 = j;
                }else if (min2 < 0 || costs[i][j] < costs[i][min2]){
                    min2 = j;
                }
            }
        }
        
        return costs[n - 1][min1];
    }
}
```
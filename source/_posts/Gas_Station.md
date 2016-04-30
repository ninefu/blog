title: Gas Station
date: 2016-02-13 16:18:45
categories:
- Leetcode
tags:
- Leetcode
- Greedy
comments: true
---

There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

Note:
The solution is guaranteed to be unique.


Explanation:

* If the sum of gas is smaller than the sum of cost, then there is no solution. Otherwise, there must be a solution
* The question guarantees that the solution is unique
* The tank should never be negative
* If a car from A cannot reach C and C is the first station that A cannot reach, then any station between A and C cannot reach C either. Thus, the car can start from the next station after C.
* See [here](https://leetcode.com/discuss/4159/share-some-of-my-ideas) for proof


```java
public class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if (gas == null || cost == null){return -1;}
        int costSum = 0, gasSum = 0, index = 0, tank = 0;;
        
        for (int i = 0; i < gas.length; i++){
            costSum += cost[i];
            gasSum += gas[i];
            tank += gas[i] - cost[i];
            if (tank < 0){
                index = i + 1;
                tank = 0;
            }
        }
        
        return costSum > gasSum ? -1 : index;
    }
}
```
title: Scramble Pairs
date: 2015-12-18 11:29:32
categories:
- Interviews
tags: 
- Technical Interviews
comments: true
---

Let a pair of distinct positive integers, (i, j), be considered "scrambled" if you can obtain j by reordering the digits of i.  For example, (12345, 25341) is a scrambled pair, but (12345, 67890) is not.

Given integers A and B with the same number of digits and no leading zeroes, how many distinct scrambled pairs (i, j) are there that satisfy: A <= i < j <= B?

<!--more-->

```java
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

public class Scramble{
	
    /**
    * Calculate the number of distinct scrambled pairs within the given range
    * @param min, the minimum value
    * @param max, the maximum value 
    * @return the number of distinct scrambled pairs within the given range
    */
    public static long scrambleCalculator(int min, int max){
        // make sure min is actually smaller than max
        if (min >= max){return 0;}
		
        // cache for visited scramble integers in the range to avoid duplicate
        Set<Integer> cache = new HashSet<Integer>();
		
        // initialize total scrambled pair count
        long count = 0;
		
        // for each integer in the range:
        for (int i = min; i <= max; i++){
            // if this integer is not in the cache, then we haven't calculated
            // the number of its scrambled pairs:
            if (!cache.contains(i)){
				
            //convert to digits
            List<Integer> digits = intToDigits(i);
				
            //compute permutation for this combination of digits
            Set<Integer> res = new HashSet<Integer>();
            permutation(res, digits, min, max, 0, 0, digits.size());
				
            // compute pair count and update total count
            count += countPairs((long) res.size());
				
            // add permutations into the cache
            if (res.size() > 1){
                cache.addAll(res);
            }
        }
    }
    return count;
    }
	
    /**
    * Recursively visit the digits combination and get the permutations of the given
    *  digits combination within the range. For example, if the digits are [1,2,3], 
    *  then we get the following permutations in order: 123, 132, 213, 231, 312, 321,
    *  assuming the range is from 100 to 999.
    * @param total, a set to store the permutations that meet the requirements
    * @param digits, a list of digits of the original number
    * @param min, the minimum value
    * @param max, the maximum value
    * @param value, a permutation of the given digits when it reaches the length of the original integer
    * @param pos, the number of digits we have "built" for a permutation
    * @param length, the number of digits in the original integer
    */
    public static void permutation(Set<Integer> total, List<Integer> digits, int min, int max, int value, int pos, int length){
        // we have "rebuilt" a new integer with the same number of digits
        if (pos == length){
            // make sure it's within the range
            if (min <= value && value <= max){
                total.add(value);
            }
            return;
        }
		
        for (int i = 0; i < digits.size(); i++){
            // avoid leading zero
            if (value != 0 || digits.get(i) != 0){
                value = value * 10 + digits.get(i);
                digits.remove(i);
                permutation(total, digits, min, max, value, pos + 1, length);
                digits.add(i, value % 10);
                value /= 10;
            }
        }
    }
	
    /**
    * Compute the count of distinct pairs of elements in a set
    * @param size, total number of elements in a set
    * @return count of distinct pairs of elements
    */
    public static long countPairs(Long size){
        // make sure there is at least one pair
        if (size < 2){return 0;}
		
        // assume we have n elements in an array, then for the first element, it can
        // form (n-1) pairs with the elements on its right; for the second 
        // element, it can form (n-2) pairs with the elements on its right without
        // duplicated pairs from the previous step..... then for the last two 
        // element, it can form 1 pair with the last one element, and for the last
        // element, it can form 0 pair. Thus, the total number of distinct pairs is
        // (0 + n - 1) * n / 2
        return (0 + size - 1) * size /2;
    }
	
	
    /**
    * Convert a positive integer to a list of digits in the integer. For
    * example, if the integer is 115, the method will return [5,1,1]
    * @param num, a positive integer.
    * @return a list of digits in the integer in reversed order
    */
    public static List<Integer> intToDigits(Integer num){
        List<Integer> ints = new ArrayList<Integer>();
        if (num == null || num < 0){return ints;}
		
        // process from the last digit to the first digit
        while (num > 0){
            int last = num % 10;
            ints.add(last);
            num /= 10;
        }
		
        return ints;
    }
	
    public static void main(String[] args){
        int min = 10000000;
        int max = 25000000;
		
        long total = scrambleCalculator(min,max);
        System.out.println(total);
    }
}
```
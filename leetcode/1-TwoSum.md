# [1. Two Sum](https://leetcode.com/problems/two-sum/)

*Easy*

# DESCRIPTION

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly*** one solution, and you may not use the same element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

# SOLUTION

## Approach 1: Brute Force

Loop through each element *x* and find if there is another value that equals to *target - x*.

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length; i++) {
            for(int j = i + 1; j < nums.length; j++)
                if(nums[i] + nums[j] == target)
                    return new int[] {i, j};
        }
        //if the result doesn't exist, it also needs to return a value
        return new int[2];
    }
}
```

**Complexity Analysis**

- Time Complexity: O(n^2)
- Space Complexity: O(1)

## Approach 2: Hash Table

To improve the time complexity, we need to find a more efficient way to check if the complement exists in the array. We can reduce the look up time from O(n) to O(1) by using hash table. It can look up in O(1) time. 

In first iteration, we add each element's value and its index to the table. Then in second iteration, we check if the element's complement exists in the table.
Beware that the complement must not be nums[i] itself.

```java
//Two-pass
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        //fill in the hash table
        for(int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        //go through each element, check their complement.
        for(int i = 0; i < nums.length; i++) {
        	//make sure the complement is not itself
            if(map.containsKey(target - nums[i]) && map.get(target - nums[i]) != i) {
            	//if it exists, return these two indices
                return new int[] {i, map.get(target - nums[i])};
            }
        }
        return new int[2];
    }
}
```
It also can be done in one-pass. While we iterate and inserting elements into the table, we also look back to check if current element's complement already exists in the table. 

```java
//One-pass
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
        	//check if the numbers ahead the current one is its complement
            if(map.containsKey(target - nums[i])) {
                return new int[] {map.get(target - nums[i]), i};
            }
            map.put(nums[i], i);
        }
        return new int[2];
    }
}
```

**Complexity Analysis**

- Time Complexity: O(n)
- Space Complexity: O(n)

# Follow Up
[15. 3Sum](3Sum.md)


# [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

*Medium*

# DESCRIPTION

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

# SOLUTION

## Approach: Dynamic Programming

First, calculate the sum of the array. If sum cannot be divisible by 2, the answer must be false. Otherwise, use dynamic programming matrix to store the result. It is a kind of 0/1 knapsack problem.

Define:

dp\[i\]\[j\] - whether the first i numbers can sum up to j.

Take [2, 1, 3] for example, dp\[2\]\[0\], dp\[2\]\[1\], dp\[2\]\[2\], dp\[2\]\[3\] should be true. Because you can choose 1, 2, neither of them(0) or both of them(3).

dp\[i\]\[j\] = dp\[i - 1\]\[j\] if you don't choose nums\[i - 1\] **OR** dp\[i - 1\]\[j - nums[i - 1]\] if you choose nums\[i - 1\].

The base cases are: 

dp\[0\]\[j\] = false since it takes nothing;

dp\[i\]\[0\] = true since if not choose any numbers, sum is 0.

Return dp\[nums.length\]\[sum / 2\]

```java
[2, 1, 3]  
  0 1 2 3 
0 T F F F
1 T F T F
2 T T T T
3 T T T T
```

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int num : nums) {
            sum += num;
        }
        if(sum % 2 != 0)
            return false;
        int m = nums.length, n = sum / 2;
        boolean[][] dp = new boolean[m + 1][n + 1];
      	//initialize
        for(int i = 0; i < m + 1; i++) {
            dp[i][0] = true;
            for(int j = 1; j < n + 1; j++) {
                dp[0][j] = false;
            }
        }
        for(int i = 1; i < m + 1; i++) {
            for(int j = 1; j < n + 1; j++) {
                if(j >= nums[i - 1]) 
                  	//take it or leave it
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
                else
                    dp[i][j] = dp[i - 1][j];
            }
        }
        return dp[m][n];
    }
}
```

**Complexity Analysis**

- Time Complexity: O(n^2)
- Space Complexity: O(n^2)
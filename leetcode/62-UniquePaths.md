# [62. Unique Paths](https://leetcode.com/problems/unique-paths/)

*Medium*

# DESCRIPTION

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)
Above is a 7 x 3 grid. How many possible unique paths are there?

**Example 1:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

**Example 2:**

```
Input: m = 7, n = 3
Output: 28
```

# SOLUTION

## Approach: Dynamic Programming

grid\[i\]\[j\] - the number of ways to reach the position \[i\]\[j\].

grid\[i\]\[j\] = grid\[i - 1\]\[j\](move right) + grid\[i\]\[j - 1\](move down)

The base cases are:

For the top and left border, it has only one way.

If i = 0 or j = 0, grid\[i\]\[j\] = 1

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] grid = new int[m][n];
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(i == 0 || j == 0)
                    grid[i][j] = 1;	//border
                else
                    //move right or move down
                    grid[i][j] = grid[i - 1][j] + grid[i][j - 1];
            }
        }
        return grid[m - 1][n - 1];
    }
}
```


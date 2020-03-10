# [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)

*Medium*

# DESCRIPTION

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Example 1:**

```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

# SOLUTION

## Approach: Dynamic Programming

grid\[i\]\[j\] - the number of ways to reach the position \[i\]\[j\].

If \[i\]\[j\] has an obstacle, grid\[i\]\[j\] = 0

Else, grid\[i\]\[j\] = grid\[i - 1\]\[j\](move right) + grid\[i\]\[j - 1\](move down)

The base cases are:

For the starter grid, if it is an obstacle, there is no way to move, return 0.

For the top border, if there is an obstacle, the grid after it should be 0.

grid\[i\]\[0\] = isObstavcle ? 0 : grid\[i - 1\]\[0\];

The same for the left border.

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] grid = new int[m][n];
        if(obstacleGrid[0][0] == 1)
            return 0;
        else
            grid[0][0] = 1;
        for(int i = 1; i < m; i++) {
            grid[i][0] = obstacleGrid[i][0] == 1 ? 0 : grid[i - 1][0];
        }
        for(int j = 1; j < n; j++) {
            grid[0][j] = obstacleGrid[0][j] == 1 ? 0 : grid[0][j - 1];
        }
        for(int i = 1; i < m; i++) {
            for(int j = 1; j < n; j++) {
                grid[i][j] = obstacleGrid[i][j] == 1 ? 0 : grid[i - 1][j] + grid[i][j - 1];
            }
        }
        return grid[m - 1][n - 1];
    }
}
```

**Complexity Analysis**

- Time Complexity: O(m * n)
- Space Complexity: O(m * n)
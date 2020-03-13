# [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

*Hard*

# DESCRIPTION

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

**Example:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

# SOLUTION

## Approach: Sliding Window

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0)
            return new int[]{};
        int[] res = new int[nums.length - k + 1];
        res[0] = findMax(nums, 0, k);
        for(int i = 1; i < nums.length - k + 1; i++) {
            if(nums[i - 1] != res[i - 1]) {
                res[i] = Math.max(nums[i + k - 1], res[i - 1]);
            }
            else {
                res[i] = findMax(nums, i, i + k);
            }
        }
        return res;
    }
    
    public int findMax(int[] nums, int start, int end) {
        int max = Integer.MIN_VALUE;
        for(int i = start; i < end; i++) {
            max = Math.max(max, nums[i]);
        }
        return max;
    }
}
```

**Complexity Analysis**

- Time Complexity: O(n)
- Space Complexity: O(1)
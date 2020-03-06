# 136. Single Number

*Easy*

# DESCRIPTION

Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```

# SOLUTION

## Approach: Bit Manipulation

Use xor ^, since A ^ A = 0, A ^ 0 = A.

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for(int i = 0; i < nums.length; i++) {
            res ^= nums[i];
        }
        return res;
    }
}
```

**Complexity Analysis**

* Time Complexity: O(n)
* Space Complexity: O(1)
# [137. Single Number II](https://leetcode.com/problems/single-number-ii/)

*Medium*

# DESCRIPTION

Given a **non-empty** array of integers, every element appears *three* times except for one, which appears exactly once. Find that single one.

**Example 1:**

```
Input: [2,2,3,2]
Output: 3
```

**Example 2:**

```
Input: [0,1,0,1,0,1,99]
Output: 99
```

# SOLUTION

## Approach: Bit Manipulation

For example, nums=[1, 2, 2, 1, 6, 2, 1].

Convert each integer into binary, count the number of ones for each digit. Since every integer appears three times except the single one, the count numbers for each digit should be divided by 3. If some digits can't, the remainder must be the digits of the single number.

```
		0 0 1
		0 1 0
		0 1 0
		0 0 1
		1 1 0
		0 1 0
		0 0 1
---------------
		1 4 3 (Count the number of ones for each digit)
%3  	1 1 0 = 6
```



```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for(int i = 0; i < 32; i++) {	//view as 32-bit
            int count = 0;
            for(int j = 0; j < nums.length; j++) {
                if((nums[j] >> i & 1) == 1)	//whether the i-th digit from left side is 1
                    count++;
            }
            if(count % 3 != 0)	//if it can't be divided by 3
                res |= 1 << i; 	//set the i-th digit of result to 1
        }
        return res;
    }
}
```

**Complexity Analysis**

- Time Complexity: O(n)
- Space Complexity: O(1)
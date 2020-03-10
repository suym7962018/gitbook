# [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

*Medium*

# DESCRIPTION

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"
Output: "bb"
```

# SOLUTION

## Approach: Dynamic Programming

Consider the case "ababa", if we already know the "bab" is a valid palindrome, then it is obviously "ababa" is a palindrom since the left and right end letters are the same.

Define:

dp\[i\]\[j\] - whether substring starting at index i and ending at index j is a palindrome.

dp\[i\]\[j\] = dp\[i + 1\]\[j - 1\] AND s\[i\] == s\[j\] 

The base cases are: 

dp\[i\]\[i\] = true, dp\[i\]\[i + 1\] = (s\[i\] == s\[i + 1\] )

Find maximum distance between i and j when dp\[i\]\[i\] = true, return the substring.

```java
    0 1 2 3 4  
    b a b a d
0 b 1 0 1 0 0
1 a   1 0 1 0
2 b     1 0 0
3 a       1 0
4 d         1
```

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s == null || s.length() == 0)
            return "";
        int n = s.length();
      	//initialize
        String res = "";
        boolean[][] dp = new boolean[n][n];
      	//DP Matrix, from bottom to up
        for(int i = n - 1; i >= 0; i--) {
            for(int j = i; j < n; j++) {
              	//when the string has 1 letter, it is always true
              	//when the string has 2 letters, it is true if 2 letters are the same
              	//when the string has more than 2 letters, it depends on whenther the letters at index i and index j are the same, and its bottom-left corner
                if(s.charAt(i) == s.charAt(j) && (j - i < 2 || dp[i + 1][j - 1]))
                    dp[i][j] = true;
              	//check whether it is the maximum length
                if(dp[i][j] && j - i + 1 > res.length())
                    res = s.substring(i, j + 1);
            }
        }
        return res;
    }
}
```

**Complexity Analysis**

- Time Complexity: O(n^2)
- Space Complexity: O(n^2)
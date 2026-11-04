# Leetcode_Day95
# Day 95 — Interleaving String

**LeetCode 97 | Medium | Java**

## Problem

Given three strings `s1`, `s2`, and `s3`, determine whether `s3` can be formed by interleaving `s1` and `s2`.

An interleaving means:
- Characters from both strings must maintain their original order.
- We can pick characters alternately or take multiple consecutive characters from either string.
- Every character from both strings must be used exactly once.

### Example

Input:
```text
s1 = "aabcc"
s2 = "dbbca"
s3 = "aadbbcbcac"
```

Output:
```text
true
```

---

## Approach: Dynamic Programming (2D DP)

I used a **2D Dynamic Programming** approach to solve this problem.

First, I check whether the combined lengths of `s1` and `s2` equal the length of `s3`. If they don't match, the answer is immediately `false`.

Then, I create a 2D boolean array:

`dp[n+1][m+1]`

Where:
- `n` is the length of `s1`.
- `m` is the length of `s2`.
- `dp[i][j]` tells us whether the first `i` characters of `s1` and the first `j` characters of `s2` can form the first `i+j` characters of `s3`.

### Steps

1. Initialize `dp[0][0] = true` because two empty strings can form an empty string.
2. Traverse the DP table using nested loops.
3. Check whether the current character of `s1` matches the corresponding character of `s3`.
4. Similarly, check whether the current character of `s2` matches the corresponding character of `s3`.
5. If either path is valid, mark the current DP state as `true`.
6. Finally, return `dp[n][m]`.

### Java Code

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {

        if(s1.length() + s2.length() != s3.length()) {
            return false;
        }

        int n = s1.length();
        int m = s2.length();

        boolean dp[][] = new boolean[n+1][m+1];
        dp[0][0] = true;

        for(int i=0; i<=n; i++) {
            for(int j=0; j<=m; j++) {

                if(i>0 && s1.charAt(i-1)==s3.charAt(i+j-1)) {
                    dp[i][j] = dp[i][j] || dp[i-1][j];
                }

                if(j>0 && s2.charAt(j-1)==s3.charAt(i+j-1)) {
                    dp[i][j] = dp[i][j] || dp[i][j-1];
                }
            }
        }

        return dp[n][m];
    }
}
```

---

## Complexity Analysis

**Time Complexity: O(n × m)**

We visit every cell in the 2D DP table once.

**Space Complexity: O(n × m)**

We use a 2D boolean array of size `(n+1) × (m+1)`.

---

## What I Learned

- How to use a 2D DP table to solve string problems.
- How one problem can have multiple possible paths.
- How to maintain the original order of characters while combining strings.
- How to use previous DP states to calculate the current state.

## Key Takeaway

Sometimes reaching the correct answer isn't about finding just one path. It's about checking whether at least one valid path exists.

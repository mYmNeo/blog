---
title: Climbing Stairs
tags:
  - leetcode
  - algorithm
date: 2016-05-05 11:15:11
---
{% blockquote %}
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
{% endblockquote %}
<!-- more -->
### Analysis:
DP的入门题

formula: dp[i] = dp[i - 1] + dp[i - 2];
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int climbStairs(int n) {
      int a = 1, b = 1;
      while (n--) {
        a = (b += a) - a;
      }
      return a;
    }
};
```

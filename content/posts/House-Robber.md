---
title: House Robber
tags:
  - leetcode
  - algorithm
date: 2016-05-06 16:38:48
---
{% blockquote %}
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night.**

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police.**
{% endblockquote %}
<!-- more -->
### Analysis:
1d DP问题

formula:

dp[i] = max(dp[i - 2] + data[i], dp[i - 1])
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (n)$

optimized $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 0) {
            return 0;
        }
        
        std::vector<int> dp(nums.size() + 1, 0);
        
        dp[0] = 0;
        for (int i = 0; i < (int) nums.size(); ++i) {
            dp[i + 1] = std::max(dp[i], (i > 1 ? dp[i - 1] : 0) + nums[i]);
        }
        
        return dp.back();
    }
};
```
optimized:
```cpp
class Solution {
public:
    int rob(vector<int>& nums) { 
        int n = nums.size(), pre = 0, cur = 0;
        for (int i = 0; i < n; i++) {
            int temp = max(pre + nums[i], cur);
            pre = cur;
            cur = temp;
        }
        return cur;
    }
};
```

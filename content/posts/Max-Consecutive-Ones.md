---
title: Max Consecutive Ones
tags:
  - leetcode
  - algorithm
date: 2017-04-19 21:25:46
---
{% blockquote %}
Given a binary array, find the maximum number of consecutive 1s in this array.

Example 1:
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
Note:

The input array will only contain 0 and 1.
The length of input array is a positive integer and will not exceed 10,000
{% endblockquote %}
<!-- more -->
### Analysis:
简单的数组问题
### Time and space complexity:
time: $\Theta (n)$
 
space: $\Theta (n)$
### Code:
```cpp
#ifdef CONFIG_H
#include "../config.h"
#endif

class Solution {
 public:
  int findMaxConsecutiveOnes(vector<int>& nums) {
    int max_length = 0;
    int i, j;

    for (i = 0; i < nums.size(); ++i) {
      j = i;

      if (!nums[j]) {
        continue;
      }

      while (j < nums.size() && nums[j]) {
        ++j;
      }

      max_length = max(max_length, j - i);
      i = j;
    }

    return max_length;
  }
};
```

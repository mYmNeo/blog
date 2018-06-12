---
title: Contains Duplicate II
tags:
  - leetcode
  - algorithm
date: 2016-05-09 16:18:46
---
{% blockquote %}
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.
{% endblockquote %}
<!-- more -->
### Analysis:
长度为k的滑动窗口,用map来记录数字出现的次数
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        int size = nums.size();
        unordered_map<int, int> record;
        for (int i = 0; i < size; ++i) {
            if (i > k) {
                --record[nums[i - k - 1]];
            }
            ++record[nums[i]];
            if (record[nums[i]] > 1) {
                return true;
            }
        }
        return false;
    }
};
```

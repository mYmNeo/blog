---
title: Remove Duplicates from Sorted Array
tags:
  - leetcode
  - algorithm
date: 2016-05-07 10:18:30
---
>
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,

Given input array nums = `[1,1,2]`,

Your function should return length = `2`, with the first two elements of nums being `1` and `2` respectively. It doesn't matter what you leave beyond the new length.
>

### Analysis:
还是去重复的思路
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (!nums.size()) {
            return 0;
        }
        
        int pos = -1;
        int last = nums.front() - 1;
        
        for (int& n : nums) {
            if (last != n) {
                nums[++pos] = n;
                last = n;
            }
        }
        
        return pos + 1;
    }
};
```

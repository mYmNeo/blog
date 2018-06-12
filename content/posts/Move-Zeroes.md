---
title: Move Zeroes
date: 2016-04-30 09:03:35
tags: 
    - leetcode
    - algorithm
---
>Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.
>
>For example, given `nums = [0, 1, 0, 3, 12]`, after calling your function, `nums` should be `[1, 3, 12, 0, 0]`.
>
>**Note:**
>1. You must do this **in-place** without making a copy of the array.
>1. Minimize the total number of operations.
<!-- more -->
### Analysis:
可以看做是排序的一种变形,in-place排序有冒泡,快排,题目要求最小的操作,冒泡显然不合适,所以用快排的partition函数
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int last = 0, cur = 0;
        
        while (cur < (int)nums.size()) {
            if (nums[cur]) {
                swap(nums[last], nums[cur])
                ++last;
            }
            ++cur;
        }
    }
};
```
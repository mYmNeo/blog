---
title: Remove Element
tags:
  - leetcode
  - algorithm
date: 2016-05-07 09:59:49
---
>
>Given an array and a value, remove all instances of that value in place and return the new length.
>
>Do not allocate extra space for another array, you must do this in place with constant memory.
>
>The order of elements can be changed. It doesn't matter what you leave beyond the new length.
>
>**Example:**
>
>Given input array nums = `[3,2,2,3]`, val = `3`
>
>Your function should return length = 2, with the first two elements of nums being 2.
>

### Analysis:
跟去重复数字一个原理.
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int pos = -1;
        for (int& n : nums) {
            if (n != val) {
                nums[++pos] = n;
            }
        }
        
        return pos + 1;
    }
};
```

---
title: Find All Numbers Disappeared in an Array
tags:
  - leetcode
  - algorithm
date: 2017-04-19 21:03:13
---
>
>Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others >appear once.
>
>Find all the elements of [1, n] inclusive that do not appear in this array.
>
>Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.
>
>Example:
>
>Input:
>[4,3,2,7,8,2,3,1]
>
>Output:
>[5,6]
>

### Analysis:
一种方式像Union Find一样,每个元素是不是属于当前这个slot,如果不是就和该元素应该属于的位置交换,直到满足条件.

另外一种方式, 先遍历一遍标记当前元素应该在的位置上的元素为负数,再遍历一遍,如果该位置的元素仍然是大于0的数,那么该元素就是缺失元素
### Time and space complexity:
time: $\Theta (n)$
 
space: $\Theta (1)$
### Code:
```cpp
#ifdef CONFIG_H
#include "../config.h"
#endif

class Solution {
 public:
  vector<int> findDisappearedNumbers(vector<int>& nums) {
    for (int i = 0; i < nums.size(); ++i) {
      int change;
      while (nums[i] != i + 1) {
        change = nums[i] - 1;
        if (nums[change] != change + 1) {
          swap(nums[change], nums[i]);
          continue;
        }
        break;
      }
    }

    vector<int> ret;
    for (int i = 0; i < nums.size(); ++i) {
      if (i + 1 != nums[i]) {
        ret.push_back(i + 1);
      }
    }

    return ret;
  }
};
```

```cpp
#ifdef CONFIG_H
#include "../config.h"
#endif

class Solution {
 public:
  vector<int> findDisappearedNumbers(vector<int>& nums) {
    int index;
    for (int i = 0; i < nums.size(); ++i) {
      index = abs(nums[i]) - 1;
      if (nums[index] > 0) {
        nums[index] = -nums[index];
      }
    }

    vector<int> ret;
    for (int i = 0; i < nums.size(); ++i) {
      if (nums[i] > 0) {
        ret.push_back(i + 1);
      }
    }

    return ret;
  }
};
```

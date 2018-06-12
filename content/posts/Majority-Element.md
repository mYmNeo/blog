---
title: Majority Element
date: 2016-04-30 09:55:43
tags:
    - leetcode
    - algorithm
---
>Given an array of size n, find the majority element. The majority element is the element that appears more than `⌊ n/2 ⌋` times.
>
>You may assume that the array is non-empty and the majority element always exist in the array.
### Analysis:
最简单的方式是统计没有数字出现的次数,然后遍历一遍统计值,找出大于`⌊ n/2 ⌋`的那个数字.
还有一种更快速地方法`Moore Voting`,思路如下,用一个统计值表示当前的major出现的次数,然后遍历数组重复如下步骤:
1. 如果统计值为0,更改major的值为当前值和统计值为1
1. 如果统计值不为0,那么如果当前值和major的值不一致,统计值就-1,否则就+1
最后,major的值就为答案

### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int major = nums[0];
        int count = 1;
        for (int i = 1; i < (int) nums.size(); ++i) {
            if (!count) {
                count = 1;
                major = nums[i];
            } else {
                count += (nums[i] == major) ? 1 : -1;
            }
        }
        
        return major;
    }
};
```
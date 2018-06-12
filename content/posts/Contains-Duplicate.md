---
title: Contains Duplicate
date: 2016-04-30 09:52:37
tags: 
    - leetcode
    - algorithm
---
>Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
<!-- more -->
### Analysis:
用unordered_set记录出现的数字,如果`find`到就返回`true`
### Time and space complexity:
time: $\Theta (n) $

space: $\Theta (n) $
### Code:
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        std::unordered_set<int> record;
        
        for (int& n : nums) {
            if (record.find(n) == record.end()) {
                record.insert(n);
            } else {
                return true;
            }
        }
        
        return false;
    }
};
```
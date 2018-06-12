---
title: Strobogrammatic Number
tags:
  - leetcode
  - algorithm
date: 2016-05-05 16:36:13
---
>
>A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).
>
>Write a function to determine if a number is strobogrammatic. The number is represented as a string.
>
>For example, the numbers "69", "88", and "818" are all strobogrammatic.
>

### Analysis:
和判断palindrome string一个思路,双指针
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    bool isStrobogrammatic(string num) {
        set<pair<char, char>> lookup;

        lookup.insert(make_pair('1', '1'));
        lookup.insert(make_pair('8', '8'));
        lookup.insert(make_pair('6', '9'));
        lookup.insert(make_pair('9', '6'));
        lookup.insert(make_pair('0', '0'));
        for (int i = 0, j = num.size() - 1; i <= j; ++i, --j) {
            if (lookup.find(make_pair(num[i], num[j])) == lookup.end()) {
                return false;
            }
        }
        
        return true;
    }
};
```

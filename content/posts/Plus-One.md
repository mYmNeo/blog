---
title: Plus One
tags:
  - leetcode
  - algorithm
date: 2016-05-07 10:01:54
---
>
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.
>

### Analysis:
逆向遍历,如果当前数字是9,那么变为0,如果不是9就把该数字+1,如果全是9的话,需要把第一位变成1,然后多加一个0
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
      int n = digits.size();
      for (int i = n - 1; i >= 0; --i) {
        if (digits[i] == 9) {
            digits[i] = 0;
        } else {
            digits[i]++;
            return;
        }
      }
      digits[0] =1;
      digits.push_back(0);
    }
};
```

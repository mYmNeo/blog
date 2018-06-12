---
title: Power of Four
tags:
  - leetcode
  - algorithm
date: 2016-05-07 10:09:52
---
{% blockquote %}
Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

**Example:**

Given num = 16, return true. Given num = 5, return false.

**Follow up:**

Could you solve it without loops/recursion?
{% endblockquote %}
<!-- more -->
### Analysis:
power of 4一定是power of 2,所以先用power of 2 的验证方法来验证,然后处理特例的情况,例如
```
2 -> 10   # 10 & 01 = 0
8 -> 1000 # 1000 & 0101 = 0
32 -> 100000 # 100000 & 010101 = 0
```
是power of 2的数字再与0x55555555作and,如果不为0,就是power of 4
### Time and space complexity:
time: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
  bool isPowerOfFour(int num) {
    // first we check if the number is power of two, then we check the 1 whether is located
    // at odd position, because 4 -> 100, 16 -> 10000
    return num > 0 && (num & (num - 1)) == 0 && (num & 0x55555555) == num;
  }
};
```

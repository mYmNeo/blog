---
title: Power of Two
tags:
  - leetcode
  - algorithm
date: 2016-05-05 15:18:01
---
>
>Given an integer, write a function to determine if it is a power of two.
>

### Analysis:
快速的判断一个数是不是power of two, `n & (n - 1) == 0`

example:
```
8 -> 1000
7 -> 0111
8 & 7 = 0
```
8是power of two

或者数1的个数,只有1个1的数就是power of two
### Time and space complexity:
time: $\Theta (1) $

space:
### Code:
```cpp
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
};
```

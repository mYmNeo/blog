---
title: Number Complement
date: 2017-03-28 07:49:28
tags:
  - leetcode
  - algorithm
---
>
Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

Note:

The given integer is guaranteed to fit within the range of a 32-bit signed integer.
You could assume no leading zero bit in the integer’s binary representation.
>

## Exammple:
```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.

Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```
### Analysis:
找出大于该数的最小2的幂-1,然后与数字做异或操作.

大于某一个数字的最小2的幂:
```cpp
x |= x >> 1;
x |= x >> 2;
x |= x >> 4;
x |= x >> 8;
x |= x >> 16;
++x;
```
### Time and space complexity:
time: $\Theta (1) $

space: $\Theta (1) $
### Code:
```cpp
class Solution {
 public:
  int findComplement(int num) {
    int mask = num;
    mask |= mask >> 1;
    mask |= mask >> 2;
    mask |= mask >> 4;
    mask |= mask >> 8;
    mask |= mask >> 16;
    return num ^ mask;
  }
};
```

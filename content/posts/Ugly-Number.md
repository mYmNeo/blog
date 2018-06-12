---
title: Ugly Number
tags:
  - leetcode
  - algorithm
date: 2016-05-05 16:28:59
---
>
>Write a program to check whether a given number is an ugly number.
>
>Ugly numbers are positive numbers whose prime factors only include `2, 3, 5`. For example, `6, 8` are ugly while `14` is not ugly since it includes another prime factor `7`.
>
>Note that `1` is typically treated as an ugly number.
>

### Analysis:
对given number分别对`2,3,5`做module运算,如果有其中任何情况不为0,那么不是ugly number
### Time and space complexity:
time: $\Theta (a+b+c), number = 2^a3^b5^c$

space: $\Theta (1) $
### Code:
```cpp
class Solution {
public:
    bool isUgly(int num) {
        while (num) {
            if (num % 2 == 0) {
                num >>= 1;
            } else if (num % 3 == 0) {
                num /= 3;
            } else if (num % 5 == 0) {
                num /= 5;
            } else {
                break;
            }
        }
        
        return num == 1;
    }
};
```

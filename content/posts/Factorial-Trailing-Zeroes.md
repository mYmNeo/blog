---
title: Factorial Trailing Zeroes
tags:
  - leetcode
  - algorithm
date: 2016-05-07 10:28:21
---
>
>Given an integer n, return the number of trailing zeroes in n!.
>
>Note: Your solution should be in logarithmic time complexity.
>

### Analysis:
因为2比较多,0的个数由5的个数决定,需要注意的是5的power的数字,会包含5的个数更多,不停的除以5,并把商加起来为0的个数
### Time and space complexity:
time: $\Theta(log_5(n))$
### Code:
```cpp
class Solution {
public:
    int trailingZeroes(int n) {
        int result = 0;
        while (n) {
            n /= 5;
            result += n;

        }
        return result;
    }
};
```

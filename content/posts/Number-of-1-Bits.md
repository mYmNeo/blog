---
title: Number of 1 Bits
tags:
  - leetcode
  - algorithm
date: 2016-05-03 09:59:40
---
{% blockquote %}
Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.
{% endblockquote %}
<!-- more -->
### Analysis:
最native的方式就是不停的logical right shift,然后统计1的个数,循环次数最多为32次.更高级一点的办法是divide and conquer,先2个bit数1的个数然后再4个bit数1的个数,再8个bit数,直到数到32bit
### Time and space complexity:
time: $\Theta (1)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        n = (n & 0x55555555) + ((n >> 1) & 0x55555555);
        n = (n & 0x33333333) + ((n >> 2) & 0x33333333);
        n = (n & 0x0f0f0f0f) + ((n >> 4) & 0x0f0f0f0f);
        n = (n & 0x00ff00ff) + ((n >> 8) & 0x00ff00ff);
        n = (n & 0x0000ffff) + ((n >> 16) & 0x0000ffff);
        return n;
    }
};
```
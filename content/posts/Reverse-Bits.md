---
title: Reverse Bits
tags:
  - leetcode
  - algorithm
date: 2016-05-09 17:29:32
---
{% blockquote %}
Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as **00000010100101000001111010011100**), return 964176192 (represented in binary as **00111001011110000010100101000000**).

**Follow up:**

If this function is called many times, how would you optimize it?
{% endblockquote %}
<!-- more -->
### Analysis:
与counting bit类似,divide and conquer,先2位2位swap,然后4位4位swap
### Time and space complexity:
time: $\Theta (1)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        n = (n >> 16) | (n << 16);
        n = ((n & 0xff00ff00) >> 8) | ((n & 0x00ff00ff) << 8);
        n = ((n & 0xf0f0f0f0) >> 4) | ((n & 0x0f0f0f0f) << 4);
        n = ((n & 0xcccccccc) >> 2) | ((n & 0x33333333) << 2);
        n = ((n & 0xaaaaaaaa) >> 1) | ((n & 0x55555555) << 1);
        return n;
    }
};
```

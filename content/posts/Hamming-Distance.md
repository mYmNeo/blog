---
title: Hamming Distance
date: 2017-03-28 07:49:14
tags:
  - leetcode
  - algorithm
---
{% blockquote %}
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.
{% endblockquote %}
<!-- more -->
Note:
{% math %}
0 <= x, y < 2^{31}
{% endmath %}
### Analysis:
divide and conquer, 先1位计算,再2位计算,一直到16位
### Time and space complexity:
time: {% math %}\Theta (1) {% endmath %}

space: {% math %}\Theta (1) {% endmath %}
### Code:
```cpp
class Solution {
 public:
  int hammingDistance(int x, int y) { return pop(x ^ y); }

  int pop(int x) {
    x = ((x >> 1) & 0x55555555) + (x & 0x55555555);
    x = ((x >> 2) & 0x33333333) + (x & 0x33333333);
    x = ((x >> 4) & 0x0f0f0f0f) + (x & 0x0f0f0f0f);
    x = ((x >> 8) & 0x00ff00ff) + (x & 0x00ff00ff);
    x = ((x >> 16) & 0x0000ffff) + (x & 0x0000ffff);

    return x;
  }
};
```


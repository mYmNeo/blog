---
title: Power of Three
tags:
  - leetcode
  - algorithm
date: 2016-05-05 11:28:06
---
{% blockquote %}
Given an integer, write a function to determine if it is a power of three.

**Follow up:**

Could you do it without using any loop / recursion?
{% endblockquote %}
<!-- more -->
### Analysis:
不停的除以3直到数字变为1,并检查每次的结果module 3后是否为0

follow up:
用INT_MAX范围内最大的power of three来module被检查的数字,如果为0,则这个数字是power of three
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}, n为{% math %}\log_3 x{% endmath %}

space: {% math %}\Theta (1){% endmath %}
### Code:
```cpp
class Solution {
public:
    bool isPowerOfThree(int n) {
        while (n > 0) {
            if (n % 3 == 0) {
                n /= 3;
                continue;
            }
            break;
        }
        
        return n == 1;
    }
};
```

---
title: Excel Sheet Column Number
date: 2016-04-30 09:39:47
tags: 
    - leetcode
    - algorithm
---
{% blockquote %}
Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```
{% endblockquote %}
<!-- more -->
### Analysis:
类似于`atoi`,只不过不是10进制而是26进制
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}
### Code:
```cpp
class Solution {
public:
    int titleToNumber(string s) {
        int num = 0;
        for (char& c : s) {
            int n = c - 'A' + 1;
            num = num * 26 + n;
        }
        return num;
    }
};
```
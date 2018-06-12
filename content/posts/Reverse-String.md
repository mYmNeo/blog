---
title: Reverse String
date: 2016-04-29 14:47:02
tags: 
  - leetcode
  - algorithm
---
>Write a function that takes a string as input and returns the string reversed.
>
>**Example:**
>
>Given s = "hello", return "olleh".
<!-- more -->
### Analysis:
用头尾2个指针进行遍历,遍历的同时进行交换
### Time ans space complexity
time: {% math %}\Theta (n) {% endmath %}
### Code:
```cpp
class Solution {
public:
    string reverseString(string s) {
      int i = 0, j = (int)s.length() - 1;
      while (i < j) {
        swap(s[i++], s[j--]);
      }

      return s;
    }
};
```
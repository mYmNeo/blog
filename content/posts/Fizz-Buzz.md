---
title: Fizz Buzz
tags:
  - leetcode
  - algorithm
date: 2017-04-19 21:23:13
---
{% blockquote %}
Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:

n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
{% endblockquote %}
<!-- more -->
### Analysis:
基础题
### Time and space complexity:
time: $\Theta (n)$
 
space: $\Theta (n)$
### Code:
```cpp
#ifdef CONFIG_H
#include "../config.h"
#endif

class Solution {
 public:
  vector<string> fizzBuzz(int n) {
    vector<string> ret;

    for (int i = 1; i <= n; ++i) {
      string item;

      if (i % 3 == 0 && i % 5 == 0) {
        item = "FizzBuzz";
      } else if (i % 3 == 0) {
        item = "Fizz";
      } else if (i % 5 == 0) {
        item = "Buzz";
      } else {
        item = to_string(i);
      }

      ret.push_back(item);
    }

    return ret;
  }
};
```

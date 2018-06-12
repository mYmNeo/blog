---
title: Happy Number
tags:
  - leetcode
  - algorithm
date: 2016-05-05 15:59:11
---
{% blockquote %}
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.
{% endblockquote %}
**Example:** 19 is a happy number
{% math %}1^2 + 9^2 = 82

{% endmath %}
{% math %}8^2 + 2^2 = 68

{% endmath %}
{% math %}6^2 + 8^2 = 100

{% endmath %}
{% math %}1^2 + 0^2 + 0^2 = 1

{% endmath %}
<!-- more -->
### Analysis:
没有特别的方法,只能按照判断happy number的方法一直计算,如果是happy number,那么就最后会得到1,如果不是就会出现重复出现的数字

optimize:

根据Floyd Cycle detection,利用快慢的方法来检测是否出现重复的数字
### Time and space complexity
time: {% math %}\Theta {% endmath %}

space: {% math %}\Theta (n) {% endmath %},optimized {% math %}\Theta (1) {% endmath %}
### Code
```cpp
class Solution {
public:
    bool isHappy(int n) {
        std::unordered_set<uint64_t> record;
        
        while (n != 1) {
            if (record.find(n) != record.end()) {
                break;
            }
            record.insert(n);
            uint64_t tmp = 0;
            while (n) {
                tmp += std::pow(n % 10, 2);
                n /= 10;
            }
            n = tmp;
        }
        
        return n == 1;
    }
};
```
optimized:
```c
int digitSquareSum(int n) {
    int sum = 0, tmp;
    while (n) {
        tmp = n % 10;
        sum += tmp * tmp;
        n /= 10;
    }
    return sum;
}

bool isHappy(int n) {
    int slow, fast;
    slow = fast = n;
    do {
        slow = digitSquareSum(slow);
        fast = digitSquareSum(fast);
        fast = digitSquareSum(fast);
    } while(slow != fast);
    if (slow == 1) return 1;
    else return 0;
}
```

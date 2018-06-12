---
title: Add Digits
date: 2016-04-29 16:03:02
tags: 
    - leetcode
    - algorithm
---

>Given a non-negative integer `num`, repeatedly add all its digits until the result has only one digit.
>
>For example:
>
>Given `num = 38`, the process is like: `3 + 8 = 11`, `1 + 1 = 2`. Since `2` has only one digit, return it.
>
>**Follow up:**
>Could you do it without any loop/recursion in $\Theta (1) $ runtime?

### Analysis:
最简单的方法就是按照例子给出的一样对每个数字做加法,然后不停迭代直到最后的`num < 10`

Follow up:

通过观察可以发现如下规律:
```
0 % 9 = 0 # 0
1 % 9 = 1 # 1
...
9 % 9 = 0 # 9
10 % 9 = 1 # 1 + 0 = 1
11 % 9 = 2 # 1 + 1 = 2
```
所以解决方式就是简单的对`num`对`9`取modulo,对`0`这个数字需要特殊处理一下就可以
### Time and space complexity
time: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int addDigits(int num) {
        int mod = num % 9;
        return num == 0 ? 0 : (mod == 0 ? 9 : mod);
    }
};
```
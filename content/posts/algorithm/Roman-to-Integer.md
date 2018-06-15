---
title: Roman to Integer
date: 2016-05-02 09:24:16
tags: 
    - leetcode
    - algorithm
---
>Given a roman numeral, convert it to an integer.
>
>Input is guaranteed to be within the range from 1 to 3999.

### Analysis:
从左往右依次读取,如果当前的字符代表的值大于后面的值,就把这个值+到最后的结果,不然就-,就像找递增数列一样
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int romanToInt(string s) {
        std::map<char, int> lookup {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000},
        };
        
        int num = 0;
        int next = 0;
        for (int i = 0; i < (int) s.length(); i = next) {
            next = i + 1;
            while (next < (int) s.length() && lookup[s[next]] > lookup[s[next - 1]]) {
                ++next;
            }
            
            num += lookup[s[next - 1]];
            for (int j = i; j < next - 1; ++j) {
                num -= lookup[s[j]];
            }
        }
        
        return num;
    }
};
```
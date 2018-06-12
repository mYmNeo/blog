---
title: Palindrome Permutation
date: 2016-04-29 15:42:38
tags: 
    - leetcode
    - algorithm
---
>Given a string, determine if a permutation of the string could form a palindrome.
>
>For example,
>
>`"code"` -> false, `"aab"` -> true, `"carerac"` -> true.
<!-- more -->
### Analysis:
这个问题可以看做是简单的统计字符问题,如果字符串每个字符都是偶数个,或者只有一个字符的数量是奇数个,那么这个字符串就会是palindrome permutation
### Time and space complexity
time: {% math %}\Theta (n){% endmath %}

space: {% math %}\Theta (n){% endmath %}
### Code:
```cpp
class Solution {
public:
    bool canPermutePalindrome(string s) {
        unordered_map<char, int> count;
        for (char& c : s) {
            ++count[c];
        }
        
        int odd = 0;
        for (auto it = count.begin(); it != count.end(); ++it) {
            if (it->second % 2 == 0) {
                continue;
            }
            
            ++odd;
        }
        
        return odd <= 1;
    }
};
```
---
title: Valid Parentheses
tags:
  - leetcode
  - algorithm
date: 2016-05-09 17:22:01
---
>
>Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.
>
>The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.
>

### Analysis:
经典的用stack解决的问题
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool isValid(string s) {
        unordered_map<char, char> table {
            {'(', ')'},
            {'[', ']'},
            {'{', '}'},
        };
        
        stack<char> frame;
        for (char& c : s) {
            switch(c) {
                case '(': 
                case '[':
                case '{': {
                    frame.push(c);
                    break;
                }
                case ')':
                case ']':
                case '}': {
                    if (!frame.empty() && table[frame.top()] == c) {
                        frame.pop();
                        break;
                    } else {
                        return false;
                    }
                }
            }
        }
        return frame.empty();
    }
};
```

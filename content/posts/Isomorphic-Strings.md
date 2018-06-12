---
title: Isomorphic Strings
tags:
  - leetcode
  - algorithm
date: 2016-05-09 16:52:48
---
{% blockquote %}
Given two strings **s** and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in **s** can be replaced to get **t**.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,

Given `"egg"`, `"add"`, return true.

Given `"foo"`, `"bar"`, return false.

Given `"paper"`, `"title"`, return true.

**Note:**

You may assume both s and t have the same length.
{% endblockquote %}
<!-- more -->
### Analysis:
用2个map来做s->t和t->s的字符映射,如果有一个不满足就是为false
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}

space: {% math %}\Theta (n){% endmath %}
### Code:
```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }
        unordered_map<char, char> sm, tm;
        int size = s.length();
        for (int i = 0; i < size; ++i) {
            if (sm[s[i]] == '\0' && tm[t[i]] == '\0') {
                sm[s[i]] = t[i];
                tm[t[i]] = s[i];
                continue;
            }
            if (sm[s[i]] == t[i] && tm[t[i]] == s[i]) {
                continue;
            }
            return false;
        }
        
        return true;
    }
};
```

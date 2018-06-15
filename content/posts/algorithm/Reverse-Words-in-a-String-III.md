---
title: Reverse Words in a String III
tags:
  - leetcode
  - algorithm
date: 2017-04-19 21:46:15
---
>
>Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.
>
>Example 1:
>Input: "Let's take LeetCode contest"
>Output: "s'teL ekat edoCteeL tsetnoc"
>Note: In the string, each word is separated by single space and there will not be any extra space in the string.
>

### Analysis:
找到一个单词的分界,然后翻转,repeat
### Time and space complexity:
time: $\Theta (n)$
 
space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    string reverseWords(string s) {
        for (int i = 0; i < s.length(); i++) {
            if (s[i] != ' ') {   // when i is a non-space
                int j = i;
                for (; j < s.length() && s[j] != ' '; j++) { } // move j to the next space
                reverse(s.begin() + i, s.begin() + j);
                i = j - 1;
            }
        }
        
        return s;
    }
};
```

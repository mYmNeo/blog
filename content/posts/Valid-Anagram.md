---
title: Valid Anagram
date: 2016-04-30 09:31:31
tags: 
    - leetcode
    - algorithm
---
>Given two strings `s` and `t`, write a function to determine if t is an anagram of `s`.
>
>For example,
>`s = "anagram"`, `t = "nagaram"`, return `true`.
>`s = "rat"`, `t = "car"`, return `false`.
>
>**Note:**
>You may assume the string contains only lowercase alphabets.
>
>**Follow up:**
>What if the inputs contain unicode characters? How would you adapt your solution to such case?
<!-- more -->
### Analysis:
用统计字符来解决,follow up也可以用此方法解决
1. 出现在`s`中的字符+1
2. 出现在`t`中的字符-1
3. 遍历一遍,统计的数字,如果某个字符的统计值不为0,就返回`false`
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        std::vector<int> record(26, 0);
        
        for (char& c : s) {
            ++record[c - 'a'];
        }
        
        for (char& c : t) {
            --record[c - 'a'];
        }
                
        for (int& n : record) {
            if (n) {
                return false;
            }
        }
        
        return true;
    }
};
```
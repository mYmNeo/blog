---
title: Group Shifted Strings
tags:
  - leetcode
  - algorithm
date: 2016-05-09 14:42:22
---
{% blockquote %}
Given a string, we can "shift" each of its letter to its successive letter, for example: `"abc" -> "bcd"`. We can keep "shifting" which forms the sequence:
{% endblockquote %}
```
"abc" -> "bcd" -> ... -> "xyz"
```
{% blockquote %}
Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

For example, given: `["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"]`, 
Return:
{% endblockquote %}
```
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
```
{% blockquote %}
Note: For the return value, each inner list's elements must follow the lexicographic order.
{% endblockquote %}
<!-- more -->
### Analysis:
根据shift的pattern来当做key,string作为value,这样相同的shift的pattern就会是同一组values,然后排序一下
### Time and space complexity:
time: {% math %}\Theta (nk){% endmath %},k是字符平均长度

space: {% math %}\Theta (n){% endmath %}
### Code:
```cpp
class Solution {
public:
    vector<vector<string>> groupStrings(vector<string>& strings) {
        unordered_map<string, vector<string>> record;
        for (string& s : strings) {
            record[shift(s)].push_back(s);
        }
        
        vector<vector<string>> result;
        for (auto it : record) {
            vector<string> group = it.second;
            sort(group.begin(), group.end());
            result.push_back(group);
        }
        
        return result;
    }

    string shift(string& s) {
        string r;
        int size = s.length();
        for (int i = 1; i < size; ++i) {
            int diff = s[i] - s[i - 1];
            if (diff < 0) {
                diff += 26;
            }
            r.push_back('a' + diff);
        }
        
        return r;
    }
};
```

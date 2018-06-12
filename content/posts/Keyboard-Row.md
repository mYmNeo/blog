---
title: Keyboard Row
date: 2017-03-28 07:49:38
tags:
  - leetcode
  - algorithm
---
{% blockquote %}
Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.
{% endblockquote %}
<!-- more -->
**Example 1:**

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```

**Note:**

1. You may use one character in the keyboard more than once.
2. You may assume the input string will only contain letters of alphabet.

### Analysis:
对每一行的字母编码,`qwertyuiop`编码`001`,`asdfghjkl`编码`010`,`zxcvbnm`编码`100`,遍历每个字串的每个字母,如果都是同一行的字母,那么所有的编码做与操作都是同一个编码,不然就会是`0`

### Time and space complexity:
time: $\Theta (n*m) $

n represents number of strings, m represents length of string

space: $\Theta (1) $

### Code:
```cpp
class Solution {
 public:
  Solution() {
    lookup.resize(26);
    vector<string> rows = {"QWERTYUIOP", "ASDFGHJKL", "ZXCVBNM"};
    int index;

    for (int i = 0; i < rows.size(); ++i) {
      index = 1 << i;
      for (auto c : rows[i]) {
        lookup[c - 'A'] = index;
      }
    }
  }

 public:
  vector<string> findWords(vector<string>& words) {
    vector<string> ret;
    int id;

    for (auto str : words) {
      id = 7;
      for (auto c : str) {
        id &= lookup[toupper(c) - 'A'];
        if (id == 0) {
          break;
        }
      }

      if (id) {
        ret.push_back(str);
      }
    }

    return ret;
  }

 private:
  vector<int> lookup;
};
```
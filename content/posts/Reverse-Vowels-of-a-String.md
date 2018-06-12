---
title: Reverse Vowels of a String
tags:
  - leetcode
  - algorithm
date: 2016-05-05 17:12:17
---
>
Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**

Given s = "hello", return "holle".

**Example 2:**

Given s = "leetcode", return "leotcede".
>

### Analysis:
跟reverse string一样,只不过需要找到vowel字母后再swap
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
  string reverseVowels(string s) {
    int i = 0, j = (int)s.length() - 1;

    while (i < j) {
      while (i < (int)s.length() && !isVowels(s[i])) {
        ++i;
      }

      if (i == (int)s.length()) {
        break;
      }

      while (j >= 0 && !isVowels(s[j])) {
        --j;
      }

      if (j < 0) {
        break;
      }

      if (i < j) {
        swap(s[i++], s[j--]);
      }
    }

    return s;
  }

  bool isVowels(char &c) {
    switch (c) {
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
    case 'A':
    case 'E':
    case 'I':
    case 'O':
    case 'U':
      return true;
    default:
      break;
    }
    return false;
  }
};
```

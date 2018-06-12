---
title: Palindrome Number
tags:
  - leetcode
  - algorithm
date: 2016-05-09 14:32:58
---
{% blockquote %}
Determine whether an integer is a palindrome. Do this without extra space.
{% endblockquote %}
<!-- more -->
### Analysis:
利用回文数的特点:逆序还是原来的数解决,注意溢出问题,为了防止溢出,只需要算一半的数字即可
### Time and space complexity:
space: {% math %}\Theta (1){% endmath %}
### Code:
```cpp
class Solution {
public:
    bool isPalindrome(int x) {
      if (x<0 || (x!=0 && x%10==0)) return false;
      int rev = 0;
      while (x>rev){
        rev = rev*10 + x%10;
        x = x/10;
      }
      return (x==rev || x==rev/10);
};
```

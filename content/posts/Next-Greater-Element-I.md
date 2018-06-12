---
title: Next Greater Element I
tags:
  - leetcode
  - algorithm
date: 2017-04-19 21:28:24
---
{% blockquote %}
st array, there is no next greater number for it in the second array, so output -1.
Example 2:
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
Note:
All elements in nums1 and nums2 are unique.
The length of both nums1 and nums2 would not exceed 1000.
{% endblockquote %}
<!-- more -->
### Analysis:
利用stack记录逆序的序列,当stack的top元素小于当前读取元素的时候,就记录一下top元素的下一个元素就是当前元素,最后记录的结果查询输入的最终结果
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}
 
space: {% math %}\Theta (n){% endmath %}
### Code:
```cpp
#ifdef CONFIG_H
#include "../config.h"
#endif

class Solution {
 public:
  vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
    vector<int> ret;
    stack<int> sub;
    unordered_map<int, int> lookup;

    for (auto n : nums) {
      while (!sub.empty() && sub.top() < n) {
        lookup.insert(make_pair(sub.top(), n));
        sub.pop();
      }
      sub.push(n);
    }

    for (auto n : findNums) {
      auto test = lookup.find(n);
      if (test == lookup.end()) {
        ret.push_back(-1);
      } else {
        ret.push_back(test->second);
      }
    }

    return ret;
  }
};
```

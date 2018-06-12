---
title: Remove Duplicates from Sorted List
tags:
  - leetcode
  - algorithm
date: 2016-05-03 10:28:37
---
{% blockquote %}
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given `1->1->2`, return `1->2`.
Given `1->1->2->3->3`, return `1->2->3`.
{% endblockquote %}
<!-- more -->
### Analysis:
和数组遍历去重复一样
### Time and space complexity:
time: $\Theta (n) $

space: $\Theta (1) $
### Code:
```cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* uniq = head;
        ListNode* cur;
        while (uniq) {
            cur = uniq;
            while (cur && uniq->val == cur->val) {
                cur = cur->next;
            }
            uniq->next = cur;
            uniq = uniq->next;
        }
        return head;
    }
};
```

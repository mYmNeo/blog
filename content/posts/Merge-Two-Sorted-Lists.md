---
title: Merge Two Sorted Lists
tags:
  - leetcode
  - algorithm
date: 2016-05-05 17:06:13
---
{% blockquote %}
Merge Two Sorted Lists
{% endblockquote %}
<!-- more -->
### Analysis:
就是简单的merge
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}

space: {% math %}\Theta (1){% endmath %}
### Code:
```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode head(0);
        ListNode* pos = &head;
        while (l1 && l2) {
            if (l1->val < l2->val) {
                pos->next = l1;
                l1 = l1->next;
            } else {
                pos->next = l2;
                l2 = l2->next;
            }
            pos = pos->next;
        }
        
        pos->next = l1 ? l1 : l2;
        
        return head.next;
    }
};
```

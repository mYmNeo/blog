---
title: Remove Nth Node From End of List
tags:
  - leetcode
  - algorithm
date: 2016-05-09 16:56:47
---
>
>Given a linked list, remove the nth node from the end of list and return its head.
>
>For example,
>
>
>Given linked list: 1->2->3->4->5, and n = 2.
>
>After removing the second node from the end, the linked list becomes 1->2->3->5.
>
>**Note:**
>
>Given n will always be valid.
>Try to do this in one pass.
>

### Analysis:
双指针,类似n大小滑动窗口
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
  ListNode *removeNthFromEnd(ListNode *head, int n) {
    ListNode **t1 = &head, *t2 = head;
    for (int i = 1; i < n; ++i) {
      t2 = t2->next;
    }
    while (t2->next != NULL) {
      t1 = &((*t1)->next);
      t2 = t2->next;
    }
    *t1 = (*t1)->next;
    return head;
  }
};

```

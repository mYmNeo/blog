---
title: Swap Nodes in Pairs
tags:
  - leetcode
  - algorithm
date: 2016-05-05 17:07:39
---
>
>Given a linked list, swap every two adjacent nodes and return its head.
>
>For example,
>Given `1->2->3->4`, you should return the list as `2->1->4->3`.
>
>Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.
>

### Analysis:
利用二级指针,先swap node,然后更改指针指向的内存位置,跳到下一个位置继续
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode** pp = &head, *a, *b;
        
        while ((a = *pp) && (b = a->next)) {
            a->next = b->next;
            b->next = a;
            *pp = b;
            pp = &(a->next);
        }
        return head;
    }
};
```

---
title: Reverse Linked List
date: 2016-05-02 09:21:28
tags: 
    - leetcode
    - algorithm
---
>Reverse a singly linked list.

### Analysis:
这个没有难度,不停的往头指针加入节点就可以
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode pivot(0);
        ListNode* pos = head;
        ListNode* next = nullptr;
        while (pos) {
            next = pos->next;
            pos->next = pivot.next;
            pivot.next = pos;
            pos = next;
        }
        return pivot.next;
    }
};
```
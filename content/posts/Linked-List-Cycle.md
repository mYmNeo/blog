---
title: Linked List Cycle
tags:
  - leetcode
  - algorithm
date: 2016-05-03 10:22:02
---
>
>Given a linked list, determine if it has a cycle in it.
>
>Follow up:
>Can you solve it without using extra space?
>

### Analysis:
native方式存储所有的node节点,如果查到相同的node节点表示有cycle.

Follow up, 快慢指针追逐,一个指针每次走2步,一个指针每次走1步,如果快指针追上慢指针,说明有cycle,否则没有.快慢指针还有一个常用的功能就是找链表中点.
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow = head, *fast = head;
        
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                return true;
            }
        }
        
        return false;
    }
};
```

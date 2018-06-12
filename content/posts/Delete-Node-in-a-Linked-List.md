---
title: Delete Node in a Linked List
date: 2016-04-30 09:15:21
tags: 
    - leetcode
    - algorithm
---
>Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.
>
>Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value `3`, the linked list should become `1 -> 2 -> 4` after calling your function.
<!-- more -->
### Analysis:
将被删除元素的copy到这个元素中
### Time and space complexity:
time: {% math %}\Theta (1){% endmath %}
### Code:
```cpp
class Solution {
public:
    void deleteNode(ListNode* node) {
        *node = *node->next;
    }
};
```
---
title: Intersection of Two Linked Lists
tags:
  - leetcode
  - algorithm
date: 2016-05-09 15:49:26
---
{% blockquote %}
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
{% endblockquote %}
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```
{% blockquote %}
begin to intersect at node c1.


**Notes:**

+ If the two linked lists have no intersection at all, return null.
+ The linked lists must retain their original structure after the function returns.
+ You may assume there are no cycles anywhere in the entire linked structure.
+ Your code should preferably run in O(n) time and use only O(1) memory.
{% endblockquote %}
<!-- more -->
### Analysis:
一种方式,原理跟快慢指针找环是一个道理,将一个list的尾部加到另外一个list的头部,找到交叉部分,然后根据交叉部分来找到相交部分.

另外一种方式是,交叉遍历,如代码所示
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
  ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode *getIntersectionNode(ListNode * headA, ListNode * headB) {
      ListNode *p1 = headA;
      ListNode *p2 = headB;

      if (p1 == NULL || p2 == NULL)
        return NULL;

      while (p1 != NULL && p2 != NULL && p1 != p2) {
        p1 = p1->next;
        p2 = p2->next;

        //
        // Any time they collide or reach end together without colliding
        // then return any one of the pointers.
        //
        if (p1 == p2)
          return p1

        //
        // If one of them reaches the end earlier then reuse it
        // by moving it to the beginning of other list.
        // Once both of them go through reassigning,
        // they will be equidistant from the collision point.
        //
        if (p1 == NULL)
          p1 = headB;
        if (p2 == NULL)
          p2 = headA;
      }

      return p1;
    }
  }
};

```

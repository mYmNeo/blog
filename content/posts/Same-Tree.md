---
title: Same Tree
date: 2016-04-30 09:23:39
tags: 
    - leetcode
    - algorithm
---
>Given two binary trees, write a function to check if they are equal or not.
>
>Two binary trees are considered equal if they are structurally identical and the nodes have the same value.
<!-- more -->
### Analysis:
对2棵树做DFS遍历,2个树为same tree的条件
1. 当前2个节点都为空
1. 当前2个节点都不为空,`val`相同
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q) {
            return true;
        }
        
        if (p && q && p->val == q->val) {
            return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
        }
        
        return false;
    }
};
```

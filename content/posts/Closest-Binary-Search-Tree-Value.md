---
title: Closest Binary Search Tree Value
tags:
  - leetcode
  - algorithm
date: 2016-05-06 16:26:45
---
{% blockquote %}
Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**
Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.
{% endblockquote %}
<!-- more -->
### Analysis:
先判断target的值是在哪个分支,然后再用该分支的值与当前的root的值相比,看哪个值更接近target
### Time and space complexity:
time: {% math %}\Theta (log (n)){% endmath %}
### Code:
```cpp
class Solution {
public:
    int closestValue(TreeNode* root, double target) {
        int cur = root->val;
        TreeNode* branch = target < cur ? root->left : root->right;
        if (!branch) {
            return root->val;
        }
        int r = closestValue(branch, target);
        return abs(r - target) < abs(cur - target) ? r : cur;
    }
};
```

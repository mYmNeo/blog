---
title: Symmetric Tree
tags:
  - leetcode
  - algorithm
date: 2016-05-06 17:01:29
---
{% blockquote %}
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:
{% endblockquote %}
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
{% blockquote %}
But the following is not:
{% endblockquote %}
```
    1
   / \
  2   2
   \   \
   3    3
```
{% blockquote %}
Note:
Bonus points if you could solve it both recursively and iteratively.
{% endblockquote %}
<!-- more -->
### Analysis:
根据example,可以看出对称的位置是left->left和right->right,left->right和right->left,递归调用,检测每个子树是否为对称.
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root) {
            return true;
        }
        
        return subTreeSymmetric(root->left, root->right);
    }
private:
    bool subTreeSymmetric(TreeNode* left, TreeNode* right) {
        if (!left && !right) {
            return true;
        }
        if (!left && right) {
            return false;
        }
       
        if (left && !right) {
            return false;
        }
       
        if (left && right && left->val != right->val) {
            return false;
        }
       
        return subTreeSymmetric(left->left, right->right) && subTreeSymmetric(left->right, right->left);
    }
};
```
iterative:
```cpp
class Solution {
public:
    bool isSymmetric(TreeNode *root) {
        TreeNode *left, *right;
        if (!root)
            return true;

        queue<TreeNode*> q1, q2;
        q1.push(root->left);
        q2.push(root->right);
        while (!q1.empty() && !q2.empty()){
            left = q1.front();
            q1.pop();
            right = q2.front();
            q2.pop();
            if (NULL == left && NULL == right)
                continue;
            if (NULL == left || NULL == right)
                return false;
            if (left->val != right->val)
                return false;
            q1.push(left->left);
            q1.push(left->right);
            q2.push(right->right);
            q2.push(right->left);
        }
        return true;
    }
};
```

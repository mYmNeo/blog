---
title: Balanced Binary Tree
tags:
  - leetcode
  - algorithm
date: 2016-05-06 16:49:15
---
>Given a binary tree, determine if it is height-balanced.
>
>For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two >subtrees of every node never differ by more than 1.

### Analysis:
DFS遍历树,给每个节点一个depth值,检查左右子树的的depth值是否相差为1
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        bool result = true;
        Depth(root, result);
        return result;
    }
private:
    int Depth(TreeNode* node, bool& result) {
        if (!node) {
            return 0;
        }
        
        int leftDepth = Depth(node->left, result);
        int rightDepth = Depth(node->right, result);
        
        result &= std::abs(leftDepth - rightDepth) <= 1;
        return std::max(leftDepth, rightDepth) + 1;
    }
};
```

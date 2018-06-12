---
title: Invert Binary Tree
date: 2016-04-29 16:45:16
tags: 
    - leetcode
    - algorithm
---
>Invert a binary tree.
>
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
>to

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
<!-- more -->
### Analysis:
后序遍历树,最后交换一下左子树和右子树
### Time and space complexity
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        invert(root);
        return root;
    }
private:
    void invert(TreeNode* node) {
        if (!node) {
            return;
        }
        
        invert(node->left);
        invert(node->right);
        std::swap(node->left, node->right);
    }
};
```
---
title: Minimum Depth of Binary Tree
tags:
  - leetcode
  - algorithm
date: 2016-05-09 15:30:57
---
>
>Given a binary tree, find its minimum depth.
>
>The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
>

### Analysis:
DFS或者BFS遍历
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    int minDepth(TreeNode *root) {
        if(!root) return 0;
        if(!root->left) return 1 + minDepth(root->right);
        if(!root->right) return 1 + minDepth(root->left);
        return 1 + min(minDepth(root->left), minDepth(root->right));
    }
};
```

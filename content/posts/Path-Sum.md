---
title: Path Sum
tags:
  - leetcode
  - algorithm
date: 2016-05-09 14:54:12
---
>
>Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.
>
>For example:
>
>Given the below binary tree and `sum = 22`,
>
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```
>
>return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.
>

### Analysis:
DFS或者BFS遍历,附带参数为当前的sum值
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        return root ? pathSum(root, 0, sum) : false;
    }
    
    bool pathSum(TreeNode* node, int sum, int want) {
        if (!node) {
            return false;
        }
        if (!node->left && !node->right) {
            return (sum + node->val) == want;
        }
        
        return pathSum(node->left, sum + node->val, want) || pathSum(node->right, sum + node->val, want);
    }
};
```

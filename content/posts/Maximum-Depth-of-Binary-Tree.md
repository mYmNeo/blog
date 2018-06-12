---
title: Maximum Depth of Binary Tree
date: 2016-04-29 16:25:47
tags: 
    - leetcode
    - algorithm
---
>Given a binary tree, find its maximum depth.
>
>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

### Analysis:
DFS遍历一遍树,保存最大的`depth`
### Time and space complexity
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int depth = 0;
        recordDepth(root, 0, depth);
        return depth;
    }
private:
    void recordDepth(TreeNode* node, int curDepth, int& maxDepth) {
        if (!node) {
            maxDepth = std::max(curDepth, maxDepth);
            return;
        }
        
        recordDepth(node->left, curDepth + 1, maxDepth);
        recordDepth(node->right, curDepth + 1, maxDepth);
    }
};
```
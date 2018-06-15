---
title: Binary Tree Level Order Traversal
tags:
  - leetcode
  - algorithm
date: 2016-05-08 11:24:07
---
>
>Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
>
>For example:
>
>Given binary tree `{3,9,20,#,#,15,7}`,
>
```
    3
   / \
  9  20
    /  \
   15   7
 ```
>
>return its level order traversal as:
>
```
[
  [3],
  [9,20],
  [15,7]
]
```

### Analysis:
level遍历
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
      DFS(root, 0);
      return res;
    }
private:
    void DFS(TreeNode* root, int level) {
      if (root == NULL) return;
      if (level == res.size()) {// The level does not exist in output
          res.push_back(vector<int>()); // Create a new level
      }

      res[level].push_back(root->val); // Add the current value to its level
      DFS(root->left, level+1); // Go to the next level
      DFS(root->right,level+1);
    }
private:
    vector<vector<int> > res;
};
```

---
title: Binary Tree Level Order Traversal II
tags:
  - leetcode
  - algorithm
date: 2016-05-07 09:51:29
---
{% blockquote %}
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:

Given binary tree `{3,9,20,#,#,15,7}`,
{% endblockquote %}
```
    3
   / \
  9  20
    /  \
   15   7
```
{% blockquote %}
return its bottom-up level order traversal as:
{% endblockquote %}
```
[
  [15,7],
  [9,20],
  [3]
]
```
<!-- more -->
### Analysis:
level遍历,最后reverse
### Time and space complexity:
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
      DFS(root, 0);
      return vector<vector<int> > (res.rbegin(), res.rend());
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

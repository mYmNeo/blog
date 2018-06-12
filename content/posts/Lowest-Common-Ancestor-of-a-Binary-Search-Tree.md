---
title: Lowest Common Ancestor of a Binary Search Tree
date: 2016-05-02 09:47:23
tags: 
    - leetcode
    - algorithm
---
>
>Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.
>
>According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”
```
        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```
>For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
>

### Analysis:
根据binary search tree的特点,如果2个值都是小于根节点值,那么答案在左子树,如果都大于根节点那么答案在右子树,不然就是根节点
### Time and space complexity:
time: $\Theta(\log(n)) $

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (p -> val < root -> val && q -> val < root -> val)
            return lowestCommonAncestor(root -> left, p, q);
        if (p -> val > root -> val && q -> val > root -> val)
            return lowestCommonAncestor(root -> right, p, q);
        return root;
    }
};
```
---
title: Pascal's Triangle II
tags:
  - leetcode
  - algorithm
date: 2016-05-08 11:29:35
---
>
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return `[1,3,3,1]`.

**Note:**

Could you optimize your algorithm to use only O(k) extra space?
>

### Analysis:
思路和pascal's triangle一样
### Time and space complexity:
time: $\Theta (k^2)$

space: $\Theta (k)$
### Code:
```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> A(rowIndex+1, 0);
        A[0] = 1;
        for(int i=1; i<rowIndex+1; i++)
            for(int j=i; j>=1; j--)
                A[j] += A[j-1];
        return A;
    }
};
```

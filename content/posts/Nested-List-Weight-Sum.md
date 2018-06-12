---
title: Nested List Weight Sum
date: 2016-04-29 14:55:15
tags: 
    - leetcode
    - algorithm
---
>Given a nested list of integers, return the sum of all integers in the list weighted by their depth.
>
>Each element is either an integer, or a list -- whose elements may also be integers or other lists.
>
>**Example 1:**
>
>Given the list `[[1,1],2,[1,1]]`, return 10. (four 1's at depth 2, one 2 at depth 1)
>
>**Example 2:**
>
>Given the list `[1,[4,[6]]]`, return 27. (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4*2 + 6*3 = 27)
<!-- more -->
### Analysis:
首先`NestedInteger`类提供了一下3个接口
```cpp
// Return true if this NestedInteger holds a single integer, rather than a nested list.
bool isInteger() const;
// Return the single integer that this NestedInteger holds, if it holds a single integer
// The result is undefined if this NestedInteger holds a nested list
int getInteger() const;
 // Return the nested list that this NestedInteger holds, if it holds a nested list
 // The result is undefined if this NestedInteger holds a single integer
 const vector<NestedInteger> &getList() const;
```
根据这3个接口,我们的解决方案思路大概就是这样的:
1. `isInteger`先判断一下是不是只有一个数字
1. 如果是那么直接用`getInteger`获得的值与当前的`depth`值相乘并记录
1. 不是数字调用`getList()`,然后递归调用`depthSum`
### Time and space complexity
time: $\Theta (n)$
### Code:
```cpp
class Solution {
public:
    int depthSum(vector<NestedInteger>& nestedList) {
        return helper(nestedList, 1);
    }
    int helper(vector<NestedInteger>& list, int depth) {
        int sum = 0;
        for (auto i : list) {
            if (i.isInteger()) {
                sum += depth * i.getInteger();
            } else {
                sum += helper(i.getList(), depth + 1);
            }
        }
        return sum;
    }
};
```
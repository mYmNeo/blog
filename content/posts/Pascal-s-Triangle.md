---
title: Pascal's Triangle
tags:
  - leetcode
  - algorithm
date: 2016-05-07 10:21:22
---
>
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,

Return
>
```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

### Analysis:
类似dp, 对于每一个新行,现push 1,然后根据上一行从第二个元素开始,把上一行的当前位置的元素和它前面的元素加一起,为这个新行该位置的值
### Time and space complexity:
### Code:
```cpp
class Solution {
public:
    vector<vector<int> > generate(int numRows) {
        vector<vector<int>> r(numRows);

        for (int i = 0; i < numRows; i++) {
            r[i].resize(i + 1);
            r[i][0] = r[i][i] = 1;

            for (int j = 1; j < i; j++)
                r[i][j] = r[i - 1][j - 1] + r[i - 1][j];
        }

        return r;
    }
};
```

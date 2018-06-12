---
title: Island Perimeter
tags:
  - leetcode
  - algorithm
date: 2017-04-19 21:16:37
---
>
>You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.
>
>Example:
>
>[[0,1,0,0],
> [1,1,1,0],
> [0,1,0,0],
> [1,1,0,0]]
>
>Answer: 16
>Explanation: The perimeter is the 16 yellow stripes in the image below:
>![](https://leetcode.com/static/images/problemset/island.png)
>

### Analysis:
本质上就是计算相连正方形有多少条边, 任意2个正方形相连,会重复计算2次边长,
所以最后的答案就是(正方形总数\*4-相连的正方形数量\*2)
### Time and space complexity:
time: $\Theta (n)$
 
space: $\Theta (n)$
### Code:
```cpp
#ifdef CONFIG_H
#include "../config.h"
#endif

class Solution {
 public:
  int islandPerimeter(vector<vector<int>>& grid) {
    int island = 0, neighbour = 0;
    for (int i = 0; i < grid.size(); ++i) {
      for (int j = 0; j < grid.front().size(); ++j) {
        if (grid[i][j]) {
          ++island;
          if (i < grid.size() - 1 && grid[i + 1][j]) {
            ++neighbour;
          }
          if (j < grid.front().size() - 1 && grid[i][j + 1]) {
            ++neighbour;
          }
        }
      }
    }

    return (island << 2) - (neighbour << 1);
  }
};
```

---
title: Rectangle Area
tags:
  - leetcode
  - algorithm
date: 2016-05-09 16:33:16
---
{% blockquote %}
Find the total area covered by two **rectilinear** rectangles in a **2D** plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.
{% endblockquote %}
{% asset_img rectangle_area.png %}
{% blockquote %}
Assume that the total area is never beyond the maximum possible value of `int`.
{% endblockquote %}
<!-- more -->
### Analysis:
分cross和non-cross2种情况
### Time and space complexity:
### Code:
```cpp
class Solution {
public:
    int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int w1 = abs(A - C);
        int h1 = abs(B - D);
        int w2 = abs(E - G);
        int h2 = abs(H - F);
        int w3 = abs(min(A, E) - max(C, G));
        int h3 = abs(min(B, F) - max(D, H));
        
        // cross 
        if (w1 + w2 >= w3 && h1 + h2 >= h3) {
            return (w1 * h1 + w2 * h2) - (w1 + w2 - w3) * (h1 + h2 - h3);
        }
        
        return w1 * h1 + w2 * h2;
    }
};
```

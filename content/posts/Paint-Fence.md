---
title: Paint Fence
tags:
  - leetcode
  - algorithm
date: 2016-05-09 15:15:11
---
{% blockquote %}
There is a fence with n posts, each post can be painted with one of the k colors.

You have to paint all the posts such that no more than two adjacent fence posts have the same color.

Return the total number of ways you can paint the fence.

**Note:**

n and k are non-negative integers.
{% endblockquote %}
<!-- more -->
### Analysis:
分2种情况考虑:
+ 最后2个fences的color一样,这样就有(k-1)*f(n-2)
+ 最后2个fences的color不一样,这样就有(k-1)*f(n-1)
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}

space: {% math %}\Theta (1){% endmath %}
### Code:
```cpp
class Solution {
public:
    int numWays(int n, int k) {
        if (n == 0 || k == 0 || (k == 1 && n > 2)) {
            return 0;
        }
        
        int w1 = k, w2 = k * k;

        if (n == 1) {
            return w1;
        }
        
        if (n == 2) {
            return w2;
        }
        
        for (int i = 3; i <= n; ++i) {
            int w3 = (k - 1) * (w1 + w2);
            w1 = w2;
            w2 = w3;
        }
        
        return w2;
    }
};
```

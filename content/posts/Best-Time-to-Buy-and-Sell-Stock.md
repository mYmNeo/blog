---
title: Best Time to Buy and Sell Stock
tags:
  - leetcode
  - algorithm
date: 2016-05-05 16:43:27
---
>
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.
>

### Analysis:
遍历数组,记录到当前节点的最大值和最小值,当最小值变化后,同时更新最大值和最小值,因为前面的最大值和最小值在后面是用不到的
### Time and space complexity:
time: $\Theta (n)$

space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.empty()) {
            return 0;
        }
        
        int profit = 0;
        int low = prices.front(), high = prices.front();
        
        for (auto p : prices) {
            if (low > p) {
                profit = max(profit, high - low);
                low = high = p;
            }
            high = max(high, p);
        }
        
        return max(profit, high - low);
    }
};
```

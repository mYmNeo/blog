---
title: Maximum Size Subarray Sum Equals k
date: 2016-05-02 09:01:39
tags: 
    - leetcode
    - algorithm
---
>Given an array nums and a target value k, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.
>
>**Example 1:**
>Given nums = `[1, -1, 5, -2, 3]`, k = `3`,
>return `4`. (because the subarray `[1, -1, 5, -2]` sums to `3` and is the longest)
>
>**Example 2:**
>Given nums = `[-2, -1, 2, 1]`, k = `1`,
>return `2`. (because the subarray `[-1, 2]` sums to `1` and is the longest)
>
>**Follow Up:**
>Can you do it in {% math %}\Theta (n){% endmath %} time?
<!-- more -->
### Analysis:
最native的方式就是O(n^2)了,从每个index开始,依次找满足target的subarry.
Follow up, 用dp的方式记录从0到某一个位置的sum值和起始index,这样就能快速地求出从任意位置的长度任意subarray的sum值
### Time and space complexity:
time: {% math %}\Theta (n){% endmath %}

space: {% math %}\Theta (n){% endmath %}
### Code:
```cpp
class Solution {
public:
    int maxSubArrayLen(vector<int>& nums, int k) {
        unordered_map<int, int> record;
        record[0] = -1;
        
        int size = nums.size();
        int sum = 0;
        int len = 0;
        for (int i = 0; i < size; ++i) {
            sum += nums[i];
            if (record.find(sum) == record.end()) {
                record[sum] = i;
            }
            
            if (record.find(sum - k) != record.end()) {
                len = max(len, i - record[sum - k]);
            }
        }
        return len;
    }
};
```
---
title: Merge Sorted Array
tags:
  - leetcode
  - algorithm
date: 2016-05-09 16:15:09
---
>
>Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
>
>**Note:**
>You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.
>

### Analysis:
题目的意思是不要用额外空间,为了避免overwrite原始数据,从m+n的位置开始写,逆序遍历2个array,选择最大的那个填到对应的位置
### Time and space complexity:
time: $\Theta (m+n)$
### Code:
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int size = m + n;
        
        int i, j;
        for (i = m - 1, j = n - 1; i >= 0 && j >= 0; ) {
            if (nums1[i] > nums2[j]) {
                nums1[--size] = nums1[i];
                --i;
            } else {
                nums1[--size] = nums2[j];
                --j;
            }
        }
        
        while (i >= 0) {
            nums1[--size] = nums1[i--];
        }
        
        while (j >= 0) {
            nums1[--size] = nums2[j--];
        }
    }
};
```

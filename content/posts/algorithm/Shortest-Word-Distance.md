---
title: Shortest Word Distance
date: 2016-04-29 16:33:36
tags: 
    - leetcode
    - algorithm
---
>Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.
>
>For example,
>Assume that words = `["practice", "makes", "perfect", "coding", "makes"]`.
>
>Given word1 = `“coding”`, word2 = `“practice”`, return 3.
>Given word1 = `"makes"`, word2 = `"coding"`, return 1.
>
>Note:
>You may assume that word1 **does not equal** to word2, and word1 and word2 are both in the list.

### Analysis:
遍历一遍所有的words,记录word1和word2出现的位置,最后求一下位置的差值的绝对值
### Time and space complexity:
time: $\Theta (n)$
space: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    int shortestDistance(vector<string>& words, string word1, string word2) {
        int distance = words.size();
        int p1 = -1, p2 = -1;
        
        int pos = 0;
        for (string& s : words) {
            if (s == word1) {
                p1 = pos;
            } else if (s == word2) {
                p2 = pos;
            }
            
            if (p1 != -1 && p2 != -1) {
                distance = min(distance, abs(p1 - p2));
            }
            ++pos;
        }
        
        return distance;
    }
};
```
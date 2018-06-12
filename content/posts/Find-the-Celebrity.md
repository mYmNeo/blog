---
title: Find the Celebrity
date: 2016-04-29 17:00:08
tags: 
    - leetcode
    - algorithm
---
>Suppose you are at a party with `n` people (labeled from `0` to `n - 1`) and among them, there may exist one celebrity. The definition of a celebrity is that all the other `n - 1` people know him/her but he/she does not know any of them.
>
>Now you want to find out who the celebrity is or verify that there is not one. The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?" to get information of whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).
>
>You are given a helper function `bool knows(a, b)` which tells you whether A knows B. Implement a function `int findCelebrity(n)`, your function should minimize the number of calls to `knows`.
>
>Note: There will be exactly one celebrity if he/she is in the party. Return the celebrity's label if there is a celebrity in the party. If there is no celebrity, return -1.
<!-- more -->
### Analysis:
Celebrity的定义是别人都认识他,他不认识所有人,根据这个定义我们可以知道如果一个人认识另外一个人,那么他肯定不是Celebrity,如果他不认识另外一个人,那么他可能是Celebrity.所以我们就先用一次遍历来找出可能的Celebrity,然后我们再遍历一次,验证这个人到底是不是Celebrity.
### Time and space complexity:
time: $\Theta (n) $
### Code:
```cpp
bool knows(int a, int b);

class Solution {
public:
    int findCelebrity(int n) {
        int candidate = 0;
        for (int i = 1; i < n; ++i) {
            if (knows(candidate, i)) {
                candidate = i;
            }
        }
        
        for (int i = 0; i < n; ++i) {
            if (i != candidate && (knows(candidate, i) || !knows(i, candidate))) {
                return -1;
            }
        }
        
        return candidate;
    }
};
```
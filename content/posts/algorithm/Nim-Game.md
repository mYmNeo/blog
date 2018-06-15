---
title: Nim Game
date: 2016-04-29 15:20:05
tags: 
    - leetcode
    - algorithm
---
>You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.
>
>Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.
>
>For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

### Analysis:
这个问题其实可以简单的看做一个整除问题,如果总共的石头是4x个,也就是4的倍数,每当你拿x个石头,你的对手只要4-x个石头,这样无论如何你都不会赢,其他的情况是则是可能赢
### Time and space complexity
time: $\Theta (1)$
### Code:
```cpp
class Solution {
public:
    bool canWinNim(int n) {
        return !(n % 4 == 0);
    }
};
```
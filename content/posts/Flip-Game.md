---
title: Flip Game
date: 2016-04-29 15:54:57
tags: 
    - leetcode
    - algorithm
---
>You are playing the following Flip Game with your friend: Given a string that contains only these two characters: `+` and `-`, you and your friend take turns to flip two **consecutive** `"++"` into `"--"`. The game ends when a person can no longer make a move and therefore the other person will be the winner.
>
>Write a function to compute all possible states of the string after one valid move.
>
>For example, given `s = "++++"`, after one move, it may become one of the following states:
```json
[
  "--++",
  "+--+",
  "++--"
]
```
>If there is no valid move, return an empty list `[]`.

### Analysis:
这个就是简单的寻找连续2个`++`字符,找到后变成`--`
### Time and space complexity
time: $\Theta (n) $
### Code:
```cpp
class Solution {
public:
    vector<string> generatePossibleNextMoves(string s) {
        vector<string> result;
        
        int size = s.size() - 1;
        for (int i = 0; i < size; ++i) {
            if (s[i] == '+' && s[i] == s[i + 1]) {
                string valid(s);
                valid[i] = '-';
                valid[i + 1] = '-';
                result.push_back(valid);
            }
        }
        
        return result;
    }
};
```
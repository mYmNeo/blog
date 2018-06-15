---
title: Valid Sudoku
tags:
  - leetcode
  - algorithm
date: 2016-05-09 15:33:37
---
>
>Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).
>
>The Sudoku board could be partially filled, where empty cells are filled with the character '.'.
>
>A partially filled sudoku which is valid.
>
>**Note:**
>
>A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.
>

### Analysis:
Sudoku的要求,每个格子只能有1-9且只能出现一次
### Time and space complexity:
### Code:
```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        unordered_map<char, int> record;
        //row
        for (int i = 0; i < 9; ++i) {
            record.clear();
            for (int j = 0; j < 9; ++j) {
                if (!pass(record, board, i, j)) {
                    return false;
                }
            }
        }
        //column
        for (int j = 0; j < 9; ++j) {
            record.clear();
            for (int i = 0; i < 9; ++i) {
                if (!pass(record, board, i, j)) {
                    return false;
                }
            }
        }
        //cell
        for (int k = 0; k < 9; ++k) {
            record.clear();
            int rowBegin = (k / 3) * 3;
            int columnBegin = (k % 3) * 3;
            for (int i = rowBegin; i < rowBegin + 3; ++i) {
                for (int j = columnBegin; j < columnBegin + 3; ++j) {
                    if (!pass(record, board, i , j)) {
                        return false;
                    }
                }
            }
        }
        
        return true;
    }
    bool pass(unordered_map<char, int>& record, vector<vector<char>>& board, int i, int j) {
        record[board[i][j]]++;
        if (board[i][j] != '.' && record[board[i][j]] > 1) {
            return false;
        }
        return true;
    }
};
```

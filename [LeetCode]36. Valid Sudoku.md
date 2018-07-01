# [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

要验证数独的棋盘，就是三个标准，行没有重复，列没有重复以及3x3格子没有重复。最开始的思路是建立1*9的hash表，依据这个标准检测三次，但这样带来一个问题是需要遍历棋盘三次。但其实可以扩大hash表，只需遍历棋盘一次。

```cpp
class Solution {
public:
    bool row[9][9] = {0}; // 9行的hash
    bool col[9][9] = {0}; // 9列的hash
    bool box[9][9] = {0}; // 9个box的hash
    
    bool isValidSudoku(vector<vector<char>>& board) {
        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++){
                char c = board[i][j];
                if (c != '.'){
                    if(!row[i][c-'1']) row[i][c-'1'] = !row[i][c-'1'];
                    else return false;
                    if(!col[j][c-'1']) col[j][c-'1'] = !col[j][c-'1'];
                    else return false;
                    int idxBox = (i/3)*3+j/3; // 判定该元素属于哪个格子
                    if(!box[idxBox][c-'1']) box[idxBox][c-'1'] = !box[idxBox][c-'1'];
                    else return false;
                }
            }
        }
        return true;
    }
};
```
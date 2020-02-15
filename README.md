# Battleships in a board
## https://leetcode.com/problems/battleships-in-a-board

Given an 2D board, count how many battleships are in it. The battleships are represented with 'X's, empty slots are represented with '.'s. 

1. You may assume the following rules:
2. You receive a valid board, made of only battleships or empty slots.
3. Battleships can only be placed horizontally or vertically. In other words, they can only be made of the shape 1xN (1 row, N columns) or Nx1 (N rows, 1 column), where N can be of any size.
4. At least one horizontal or vertical cell separates between two battleships - there are no adjacent battleships.
```
Example:
X..X
...X
...X
In the above board there are 2 battleships.

Invalid Example:
...X
XXXX
...X
This is an invalid board that you will not receive - 
as battleships will always have a cell separating between them.
```
**Follow up:**

Could you do it in one-pass, using only O(1) extra memory and without modifying the value of the board?

# Implementation 1 : DFS

```java
class Solution {
    public int countBattleships(char[][] board) {
        int battleships = 0;
        if(board == null || board.length == 0)
            return battleships;
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                if(board[i][j] == 'X'){
                    battleships++;
                    sinkBattleship(board, i, j);
                }
            }
        }
        return battleships;
    }
    
    private void sinkBattleship(char[][] board, int i, int j){
        if(i < 0 || i >= board.length || j < 0 || j >= board[i].length ||
           board[i][j] == '.')
            return;
        board[i][j] = '.';
        sinkBattleship(board, i, j-1);
        sinkBattleship(board, i, j+1);
        sinkBattleship(board, i-1, j);
        sinkBattleship(board, i+1, j);
    }
}
```
# Implementation 2 
```java
class Solution {
    public int countBattleships(char[][] board) {
        int battleships = 0;
        if(board == null || board.length == 0)
            return battleships;
        for(int i = 0; i < board.length; i++){
            for (int j = 0; j < board[i].length; j++){
                if(board[i][j] == '.')
                    continue;
                if(j > 0 && board[i][j-1] == 'X')
                    continue;
                if(i > 0 && board[i-1][j] == 'X')
                    continue;
                battleships++;
            }
        }
        return battleships;
    }
}
```

# References :
https://www.youtube.com/watch?v=wBG6078g1gE

---
layout: post
author: Aniket Ambore
tags: [arrays, hashing, medium]
---

## Leetcode PS: [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

- Each row must contain the digits `1-9` without repetition.
- Each column must contain the digits `1-9` without repetition.
- Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note**:
- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

### Example 1:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```dart
Input: board = 
[["5","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]]
Output: true
```

### Example 2:

```dart
Input: board = 
[["8","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]]
Output: false
```

**Explanation**: Same as Example 1, except with the **5** in the top left corner being modified to **8**. Since there are two **8**'s in the top left `3x3` sub-box, it is invalid.

### Constraints
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or '`.`'.

# Solution

## Intuition
`List<Set>` representing Rows, Columns and Boxes will solve the problem.

## Approach
1. Checking if an element is present in the `row` is just by iterating from 1-9.
2. Similarly, Checking if an element is present in the `cols` is also just by iterating from 1-9.
3. For Boxes, that is for 3x3 grid we'll be dividing it as 0,1,2,3,4,5,6,7,8 different sets similar to `rows` and `cols`, but the formula to get the `index` of `boxes` is `3 * (r ~/ 3) + (c ~/ 3)`

## Complexity
- Time complexity: **O(9^2)**
- Space complexity: **O(9^2)**

## Code

```dart
class Solution {
  bool isValidSudoku(List<List<String>> board) {
      final rows = List<Set>.generate(9, (_) => {});
      final cols = List<Set>.generate(9, (_) => {});
      final boxes = List<Set>.generate(9, (_) => {});

      for(int r=0 ; r<9 ; r++){
          for(int c=0 ; c<9 ; c++){
              var element = board[r][c];
              if(element != '.'){
                  var boxIndex = 3 * (r ~/ 3) + (c ~/ 3);

                  if(contains(rows,r,element) ||
                  contains(cols,c,element) ||
                  contains(boxes,boxIndex,element)) return false;

              }
          }
      }

      return true;
  }

  bool contains(List<Set> setsList, int index, String element){
      if(setsList[index].contains(element)){
          return true;
      }
      setsList[index].add(element);
      return false;
  }
}
```

## Reference:
- [Valid Sudoku - Amazon Interview Question - Leetcode 36 - Python](https://www.youtube.com/watch?v=TjFXEUCMqI8)
## [单词搜索(中等)](https://leetcode-cn.com/problems/word-search/)
<div class="notranslate"><p>给定一个二维网格和一个单词，找出该单词是否存在于网格中。</p>

<p>单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。</p>

<p><strong>示例:</strong></p>

<pre>board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "<strong>ABCCED</strong>", 返回 <strong>true</strong>.
给定 word = "<strong>SEE</strong>", 返回 <strong>true</strong>.
给定 word = "<strong>ABCB</strong>", 返回 <strong>false</strong>.</pre>
</div>

## 思路
整体思路
使用深度优先搜索（DFS）和回溯的思想实现。用了一个二维数组 visited 对使用过的元素做标记。

外层：遍历  
首先遍历 board 的所有元素，先找到和 word 第一个字母相同的元素，然后进入递归流程。  
假设这个元素的坐标为 (i, j)，进入递归流程前，先记得把该元素打上使用过的标记：`visited[i][j] = true`  

内层：递归  
从 (i, j) 出发，朝它的上下左右试探，看看它周边的这四个元素是否能匹配 word 的下一个字母  
如果匹配到了：带着该元素继续进入下一个递归  
如果都匹配不到：返回 false  
当 word 的所有字母都完成匹配后，整个流程返回 True  

几个注意点  
递归时元素的坐标是否超过边界  
回溯标记 mark[i][j] = 0以及 return 的时机

## 代码
```java
class Solution {
    int row;
    int col;
    int[] arrowX = {0, 1, 0, -1};
    int[] arrowY = {-1, 0, 1, 0};

    public boolean exist(char[][] board, String word) {
        row = board.length;
        if (row == 0) {
            return false;
        }
        col = board[0].length;
        // 记录节点是否被访问过
        boolean[][] visited = new boolean[row][col];
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (board[i][j] == word.charAt(0)) {
                    if (dfs(board, word, visited, 1, i, j)) {
                        return true;
                    }
                }
            }
        }
        return false;
    }

    private boolean dfs(char[][] board, String word, boolean[][] visited, int idx, int x, int y) {
        if (idx == word.length()) {
            return true;
        }
        // 假设当前节点符合
        visited[x][y] = true;
        // 探测四个方向
        for (int i = 0; i < 4; i++) {
            int nx = x + arrowX[i];
            int ny = y + arrowY[i];
            if (nx < 0 || nx >= row || ny < 0 || ny >= col || visited[nx][ny]) {
                continue;
            }
            if (board[nx][ny] != word.charAt(idx)) {
                continue;
            }
            // 递归探测下一个节点
            if (dfs(board, word, visited, idx + 1, nx, ny)) {
                return true;
            }
        }
        // 恢复当前节点状态
        visited[x][y] = false;
        return false;
    }
}
```

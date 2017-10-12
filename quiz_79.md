##Quiz#79.md

给定一个m*n的char矩阵, 并给定一个字符串, 问是否存在该字符串的一个有效路径, 且矩阵中的每个字符只能使用一次

* 回溯法:

判断每个矩阵合法位置(下标合法且未被使用), 如果位置对应字符等于字符串当前位置字符, 继续向前, 否则取消当前位置选中状态并回退, 直到找到一条合法路径

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0) return false;
        int rows = board.length, lines = board[0].length;
        boolean[][] used = new boolean[rows][lines];
        for (int i = 0;i < rows;i++) {
            for (int j = 0;j < lines;j++) {
                if (exist(board, used, word, i, j, 0)) return true;
            }
        }
        return false;
    }
    
    public boolean exist(char[][] board, boolean[][] used, String word, int startX, int startY, int curWordPos) {
        int rows = board.length, lines = board[0].length;
        if (curWordPos == word.length()) {
        	return true;
        }
        if (startX < 0 || startX >= rows || startY < 0 || startY >= lines) {
        	return false;
        }
        if (used[startX][startY] == true){
        	return false;
        }
        
        char c = word.charAt(curWordPos);
        if (board[startX][startY] != c) {
        	return false;
        }
        used[startX][startY] = true;
        boolean res = exist(board, used, word, startX-1, startY, curWordPos+1) 
                      || exist(board, used, word, startX+1, startY, curWordPos+1)
                      || exist(board, used, word, startX, startY-1, curWordPos+1)
                      || exist(board, used, word, startX, startY+1, curWordPos+1);
        if (!res) {
        	used[startX][startY] = false;
        }
        return res;
    }
}
```
##Quiz#64

给定一个m*n的矩阵, 矩阵每个节点带有权值, 求从左上角到右下角权值最小的路径
	 
* 动态规划解: 

和Quiz#62, Quiz#63相同, 构造m*n矩阵记录每个节点经过所需的最小权值, 由于只能向右或者向下走, 同样取上边节点或者左边节点权值较小的, 最后返回(m-1, n-1)

```java
class Solution {
    public int minPathSum(int[][] grid) {
        if (grid == null || grid.length == 0) return 0;
        int rows = grid.length, lines = grid[0].length;
        int[][] sum = new int[rows][lines];
        sum[0][0] = grid[0][0];
        for (int i = 1;i < rows;i++) sum[i][0] = grid[i][0] + sum[i-1][0];
        for (int j = 1;j < lines;j++) sum[0][j] = grid[0][j] + sum[0][j-1];
        for (int i = 1;i < rows;i++) {
            for (int j = 1;j < lines;j++) {
                sum[i][j] = grid[i][j] + Math.min(sum[i-1][j], sum[i][j-1]);
            }
        }
        return sum[rows-1][lines-1];
    }
}
```
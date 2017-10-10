##Quiz#63

给定m*n矩阵, 从左上角到右下角共有多少种走法, 只能往右或者往下走, 升级版. 矩阵中出现部分障碍, 这些位置不能走

例:

	[
 	 [0,0,0],
	 [0,1,0],
	 [0,0,0]
	]
	
该输入对应的合法路径有2条

* 动态规划解:

和Quiz#62一样, 构造m*n矩阵记录每个点的可达性, 在计算左上角和右下角的路径数时, 去掉障碍点即可

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0) return 0;
        int rows = obstacleGrid.length, lines = obstacleGrid[0].length;
        
        int[][] sum = new int[rows][lines];
        if (obstacleGrid[0][0] == 1) {
            return 0;
        }
        sum[0][0] = 1;
        for (int i = 0;i < rows;i++) {
            for (int j = 0;j < lines;j++) {
                if (obstacleGrid[i][j] == 1) continue;
                if (i > 0 && obstacleGrid[i-1][j] == 0) sum[i][j] += sum[i-1][j];
                if (j > 0 && obstacleGrid[i][j-1] == 0) sum[i][j] += sum[i][j-1];
            }
        }
        return sum[rows-1][lines-1];
    }
}
```
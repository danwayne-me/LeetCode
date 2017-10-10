## Quiz#62

给定一个m*n的矩阵, 求从左上角到右下角共有多少种走法(只能向右或者向下走)

如图所示:
![图例](https://leetcode.com/static/images/problemset/robot_maze.png)

* 动态规划解:

构造m*n二维数组, 记录到达每个点的路径数目, 由于只能向右或者向下走, 因此能够到达某一个点必须先到达该点上面或者左面的点, 即到达该店的路径数目就是到达该点上面的点的路径数目和左面的点的路径数目的和, 最后将(m-1, n-1)的数字返回

```java
class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 1 || n == 1) {
            return 1;
        }
        int[][] sum = new int[m][n];
        for (int i = 0;i < m;i++) {
            sum[i][0] = 1;
        }
        for (int j = 0;j < n;j++) {
            sum[0][j] = 1;
        }
        for (int i = 1;i < m;i++) {
            for (int j = 1;j < n;j++) {
                sum[i][j] = sum[i-1][j] + sum[i][j-1];
            }
        }
        return sum[m-1][n-1];
    }
}
```
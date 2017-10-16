##Quiz#85

给定一个只包含0和1的二维矩阵, 求出其中连续1所构成的矩形的最大面积

```
1 0 1 0 0
1 0 1 1 1    --->      6
1 1 1 1 1
1 0 0 1 0
```

解法可利用quiz#84的思路, 遍历每一行, 根据其中包含1的列来维护一个全局的高度数组, 然后可将其转化为quiz#84

* 遍历解 : 

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        int rows = matrix.length, lines = matrix[0].length;
        int[] heights = new int[lines];
        int res = 0;
        for (int i = 0;i < rows;i++) {
            int max = 0;
            List<Integer> stack = new LinkedList<>();
            for (int j = 0;j < lines;j++) {
                if (matrix[i][j] == '1') {
                    heights[j]++;
                } else {
                    heights[j] = 0;
                }
            }
            for (int j = 0;j <= lines;j++) {
                int height = j == lines ? 0 : heights[j];
                if (stack.isEmpty() || height >= heights[stack.get(0)]) {
                    stack.add(0, j);
                } else {
                    int top = stack.remove(0);
                    max = Math.max(max, heights[top] * (stack.isEmpty() ? j : j-1-stack.get(0)));
                    j--;
                }
            }
            res = Math.max(res, max);
        }
        return res;
    }
}
```
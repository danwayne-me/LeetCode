## Quiz#54
给定N*M的矩阵，按照螺旋状输出所有的数字,例如：

	1 2 3
	4 5 6   ————> 1,2,3,6,9,8,7,4,5
	7 8 9
	
* 暴力解：

按照题目字面意思，依照螺旋状读取数组

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        if (matrix == null) {
            return null;
        }
        if (matrix.length == 0) {
            return new ArrayList<Integer>();
        }
        int rows = matrix.length;
        int lines = matrix[0].length;
        int top = 0, left = 0, right = lines - 1, bottom = rows - 1;
        int i = top, j = left;
        List<Integer> res = new ArrayList<>();
        while (true) {
            while (j <= right) {
                res.add(matrix[i][j++]);
            }
            i = ++top;
            j = right;
            if (top > bottom) {
                break;
            }
            while (i <= bottom) {
                res.add(matrix[i++][j]);
            }
            j = --right;
            i = bottom;
            if (left > right) {
                break;
            }
            while (j >= left) {
                res.add(matrix[i][j--]);
            }
            i = --bottom;
            j = left;
            if (top > bottom) {
                break;
            }
            while (i >= top) {
                res.add(matrix[i--][j]);
            }
            j = ++left;
            i = top;
            if (left > right) {
                break;
            }
        }
        return res;
    }
}
```
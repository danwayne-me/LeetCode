## Quiz#59

旋转矩阵2, 给定一个正整数N, 按照顺时针螺旋的方式将1~N<sup>2</sup>填入矩阵并返回

例: N=3时, 输出

	[
	 [ 1, 2, 3 ],
 	 [ 8, 9, 4 ],
	 [ 7, 6, 5 ]
	]
	
* 暴力解:

和Quiz#54相同, 构建N*N矩阵之后, 依照字面意思, 螺旋填入数字

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int left = 0, top = 0, right = n - 1, bottom = n - 1;
        int number = 1;
        int i = top, j = left;
        while (left <= right && top <= bottom) {
            while (j <= right) res[i][j++] = number++;
            i = ++top; j =  right;
            while (i <= bottom) res[i++][j] = number++;
            j = --right; i = bottom;
            while (j >= left) res[i][j--] = number++;
            i = --bottom; j = left;
            while (i >= top) res[i--][j] = number++;
            j = ++left; i = top;
        }
        return res;
    }
}
```
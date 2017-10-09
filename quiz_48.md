## Quiz#48
给定N*N矩阵，顺时针旋转90度

```java
class Solution {
    public void rotate(int[][] matrix) {
        
    }
}
```

* 暴力解：

对于输入的N*N的二维数组，创建一个相同的二位数组， 用来保存旋转后的数据， 然后以横纵坐标将值赋给输入， 完成旋转

```java
class Solution {
    public void rotate(int[][] matrix) {
        if (matrix == null) {
            return;
        }
        int size = matrix.length;
        int[][] res = new int[size][size];
        
        for (int i = 0;i < size;i++) {
            for (int j = 0;j < size;j++) {
                res[j][size - 1 - i] = matrix[i][j];
            }
        }
        
        for (int i = 0;i < size;i++) {
            for (int j = 0;j < size;j++) {
                matrix[i][j] = res[i][j];
            }
        }
    }
}
```

* 通用解：

对于任意N*N矩阵，可以将旋转操作转化为翻转操作，顺时针旋转90度可以上下翻转之后再沿左上右下对角线翻转， 其他角度翻转同理（可以自己拿一个正方形纸片验证）

**验证要点：用四个顶点带着边进行操作，找准四个顶点的位置即可实现旋转**

```java
class Solution {
    public void rotate(int[][] matrix) {
        if (matrix == null) {
            return;
        }
        
        int size = matrix.length;
        int tmp;
        for (int i = 0;i < size / 2;i++) {
            for (int j = 0;j < size;j++) {
                tmp = matrix[i][j];
                matrix[i][j] = matrix[size - 1 - i][j];
                matrix[size - 1 - i][j] = tmp;
            }
        }
        
        for (int i = 0;i < size;i++) {
            for (int j = i + 1;j < size;j++) {
                tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
    }
}
```

##Quiz#73

给定m*n矩阵，如果其中存在0， 则把该元素所在的行和列全都置为0
*要求：空间复杂度越小越好*

* 记录所有0元素的位置（ O(m*n) ）：

```
将所有出现的0的位置都记录下来，然后把所有涉及的行和列置为0
```	

* 记录所有的行和列（ O(m +n) ) ：

```
将所有0所属于的行和列都记录下来，然后依次置为0，和上个方法相比，该方法的主要优势是记录数据的去重
```

* 按行遍历，记录所有的列（ O(Math.min(m,n)) ）：

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return;
        int rows = matrix.length, lines = matrix[0].length;
        int[] blank = new int[lines];
        for (int i = 0;i < rows;i++) {
            boolean clear = false;
            for (int j = 0;j < lines;j++) {
                if (matrix[i][j] == 0) {
                    blank[j] = 1;
                    clear = true;
                }
            }
            if (clear) {
                for (int j = 0;j < lines;j++) {
                    matrix[i][j] = 0;
                }
            }
        }
        for (int j = 0;j < lines;j++) {
            if (blank[j] == 1) {
                for (int i = 0;i < rows;i++) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

* 利用第一行和第一列进行标记（ O(1) ）：

**该题目的难点是如何在将某元素置为0之后进行合理的标记，方式后续再次处理而导致错误**， 将第一行和第一列作为索引行列进行标记，所有为0的元素，将其所在行列与第一行和第一列的交点元素置为0，第一行和第一列本身的元素索引用两个额外的变量进行标记，即可实现在O(1)的空间复杂度下完成。

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return;
        int rows = matrix.length, lines = matrix[0].length;
        boolean clearRow = false, clearLine = false;
        for (int i = 0;i < rows;i++) {
            for (int j = 0;j < lines;j++) {
                if (matrix[i][j] == 0) {
                    if (i == 0) clearRow = true;
                    if (j == 0) clearLine = true;
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for (int i = 1;i < rows;i++) {
            for (int j = 1;j < lines;j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
        if (clearRow) {
            for (int j = 0;j < lines;j++) {
                matrix[0][j] = 0;
            }
        }
        if (clearLine) {
            for (int i = 0;i < rows;i++) {
                matrix[i][0] = 0;
            }
        }
    }
}
```

	
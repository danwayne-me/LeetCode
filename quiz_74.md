##Quiz#74

给定一个二维数组，数组每行从左到右递增，每一行第一个元素比上一个元素大，给出一个高效的查找算法

* 暴力解：

首先根据每一行的首位元素确定目标元素所在行数，然后在行内二分查找

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return false;
        int rows = matrix.length, lines = matrix[0].length;
        int pos = -1;
        for (int i = 0;i < rows;i++) {
            if (matrix[i][0] <= target && matrix[i][lines-1] >= target) {
                pos = i;
                break;
            }
        }
        if (pos == -1) return false;
        return binarySearch(matrix[pos], target);
    }
    
    public boolean binarySearch(int[] numbers, int target) {
        int start = 0, end = numbers.length - 1;
        if (target == numbers[start] || target == numbers[end]) return true;
        
        int middle;
        while (start <= end) {
            middle = (start + end) / 2;
            if (target == numbers[middle]) return true;
            if (target > numbers[middle]) {
                start = middle + 1;
            } else {
                end = middle - 1;
            }
        }
        return false;
    }
}
```
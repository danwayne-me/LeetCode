#Quiz#119 

给定行序号, 计算得出杨辉三角的对应行

和Quiz#118 类似, 只不过在构造杨辉三角的时候不再借助额外的数组, 直接在当前数组将相邻元素相加并更新

* 暴力解: 

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> res = new ArrayList<>();
        rowIndex += 1;
        int init = Math.min(2, rowIndex);
        for (int i = 0;i < init;i++) {
            res.add(1);
        }
        for (int i = 2;i < rowIndex;i++) {
            int last = 1;
            for (int j = 1;j < i;j++) {
                int tmp = res.get(j) + last;
                last = res.get(j);
                res.set(j, tmp);
            }
            res.add(1);
        }
        return res;
    }
}
```
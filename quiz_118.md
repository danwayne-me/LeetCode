##Quiz#118

输入行数, 构建n行的杨辉三角

* 暴力解:

根据杨辉三角的定义, 直接构建

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<>();
        int init = Math.min(2, numRows);
        for (int i = 1 ;i <= init;i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0;j < i;j++) {
                list.add(1);
            }
            res.add(list);
        }
        for (int i = 3;i <= numRows;i++) {
            List<Integer> list = new ArrayList<>();
            list.add(1);
            List<Integer> ref = res.get(res.size() - 1);
            for (int j = 1;j < i-1;j++) {
                list.add(ref.get(j-1) + ref.get(j));
            }
            list.add(1);
            res.add(list);
        }
        return res;
    }
}
```
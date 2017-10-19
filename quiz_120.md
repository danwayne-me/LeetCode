##Quiz#120 

给定一个只包含整数的三角, 求从三角的顶端到底部的一条和最短的路径

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
输出11 : 2 -> 3 -> 5 -> 1
```

* 动归解:

利用输入数据, 进行每一层的和记录, 最后输出最后一层和的最小值

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int sum = Integer.MAX_VALUE;
        if (triangle == null || triangle.size() == 0) return sum;
        List<Integer> step = triangle.get(0);
        for (int i = 1;i < triangle.size();i++) {
            List<Integer> tmp = triangle.get(i);
            tmp.set(0, tmp.get(0) + step.get(0));
            int size = tmp.size();
            tmp.set(size-1, tmp.get(size-1) + step.get(step.size()-1));
            for (int j = 1;j < size-1;j++) {
                tmp.set(j, tmp.get(j) + Math.min(step.get(j-1), step.get(j)));
            }
            step = tmp;
        }
        for (int i = 0;i < step.size();i++) {
            if (sum > step.get(i)) sum = step.get(i);
        }
        return sum;
    }
}
```
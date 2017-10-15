##Quiz#84
给定一个柱形图，求出其中所包含的最大矩形

例如：

![](https://leetcode.com/static/images/problemset/histogram.png)

所得到的最大矩形为：

![](https://leetcode.com/static/images/problemset/histogram_area.png)

该题目的难点是如何同时记录矩形的高度和该高度对应的有效区间

* 利用栈记录高度对应有效区间解法：

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null) return 0;
        int length = heights.length;
        int max = 0;
        List<Integer> stack = new LinkedList<>();
        for (int i = 0;i <= length;i++) {
            int height = i == length ? 0 : heights[i];
            if (stack.isEmpty() || height >= heights[stack.get(0)]) {
                stack.add(0, i);
            } else {
                int top = stack.remove(0);
                max = Math.max(max, heights[top] * (stack.isEmpty() ? i : i-1-stack.get(0)));
                i--;
            }
        }
        return max;
    }
}
```
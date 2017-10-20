##Quiz#123

给定一组包含整数的数组代表股票价格, 当最多允许交易两次的时候, 计算最大收益

当允许多次交易的时候, 可以采取线性思维, 记录当前收益, 每一次交易买入从当前收益中扣除与价格对等的收益, 卖出加上与价格相等的收益, 最后返回总收益即可

* 暴力解(最多允许k次通解):

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int k = 2;
        int[][] profit = new int[k][2];
        for (int i = 0;i < profit.length;i++) {
            profit[i][0] = Integer.MIN_VALUE;
        }
        for (int i = 0;i < prices.length;i++) {
            for (int j = 0;j < profit.length;j++) {
                profit[j][0] = j == 0 ? Math.max(profit[j][0], -prices[i]) :
                                        Math.max(profit[j][0], profit[j-1][1] - prices[i]);
                profit[j][1] = Math.max(profit[j][1], prices[i] + profit[j][0]);
            }
        }
        return profit[profit.length-1][1];
    }
}
```
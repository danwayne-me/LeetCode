##Quiz#121

给定一个整数数组分别代表股票每天的价格, 当只允许交易一次时, 求出最大利润

记录股票当前的最低值, 今儿求出当前的最大利润, 返回全局最大利润即可

* 暴力解:

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int min = prices[0];
        int profit = 0;
        for (int i = 1;i < prices.length;i++) {
            min = Math.min(min, prices[i]);
            profit = Math.max(profit, prices[i] - min);
        }
        return profit;
    }
}
```
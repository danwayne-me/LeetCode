##Quiz#122

给定一组整数代表股票每天的价格, 允许多次交易, 求出可获得的最大利润

在每次股票跌之前卖出即可

* 暴力解: 

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int min = prices[0], length = prices.length, profit = 0;
        for (int i = 1;i <= length;i++) {
            int currentPrice = i == length ? 0 : prices[i];
            if (currentPrice >= prices[i-1]) continue;
            profit += prices[i-1] - min;
            min = currentPrice;
        }
        return profit;
    }
}
```
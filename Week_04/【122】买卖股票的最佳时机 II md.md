### 122. Best Time to Buy and Sell Stock II

**Difficulty:** Easy

#### 方法一：贪心算法

由于交易次数不限，因此可以比较相邻两天的股票价格，如果后一天的股票价格高于前一天的股票价格，则将两天的股票价格之差计入总利润。

贪心算法并不是模拟真正的交易过程，只是用于计算最大利润。

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if prices is None  or len(prices) < 2:
            return 0
        profit = 0
        for i in range(len(prices)-1):
            if (prices[i+1] - prices[i] > 0):
                profit += (prices[i+1] - prices[i])
        return profit
```

**复杂度分析**

- 时间复杂度：O(n)，其中n是数组的长度。遍历数组一次。

- 空间复杂度：O(1)。

#### 方法二：动态规划

可以用贪心算法做的题通常也可以用动态规划做。这道题的动态规划需要定义以下要素。

1. 状态定义：每一天都可能有两种状态，持有现金或持有股票，分别用 `cash` 和 `stock` 表示。

2. 状态转移：`cash[i] = Math.max(cash[i - 1], stock[i - 1] + prices[i]`，`stock[i] = Math.max(stock[i - 1], cash[i - 1] - prices[i])`。

3. 边界情况：`cash[0] = 0`，`stock[0] = -prices[0]`。

最后一天的两种状态中，显然持有现金比持有股票的利润更大，因此最终结果是最后一天的持有现金状态的值。

由于每天的状态只依赖于前一天的状态，因此可以使用滚动数组优化空间复杂度。

```
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int cash = 0, stock = -prices[0];
        int length = prices.length;
        for (int i = 1; i < length; i++) {
            int nextCash = Math.max(cash, stock + prices[i]);
            int nextStock = Math.max(stock, cash - prices[i]);
            cash = nextCash;
            stock = nextStock;
        }
        return cash;
    }
}
```

**复杂度分析**

- 时间复杂度：O(n)，其中n是数组的长度。遍历数组一次。

- 空间复杂度：O(1)。

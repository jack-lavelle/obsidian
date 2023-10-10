```Python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Initialize defaults. `buy_price` set to maximum since we want it to be overridden 
        # (which it *will* be in the first conditional), and `max_profit` set to 0 since
        # we want it to be overridden but *only* if the profit > 0 (not `float("-inf")` since
        # not buying anything is an option).

        buy_price = float("inf")
        max_profit = 0

        # begin to iterate through the prices
        for price in prices:
            # if a price is lower than the current `buy_price`, switch them.
            if price < buy_price:
                buy_price = price

            # Firstly, the fact we have not gone to the first conditional means we are dealing
            # with the previous `buy_price`. Therefore, it is `sell_price` that could be changed.
            # If the new profit from this new `sell_price` is greater than previous profit, overwrite
            # the profit.

            # In this way, we have taken care of minimizing the `buy_price`, and maximizing the `sell_price`.
            elif price - buy_price > max_profit:
                max_profit = price - buy_price

        # After having gone through the prices, return `max_profit` which is, at least, 0.
        return max_profit
```

- [ ] write the solution for *Best Time to Buy and Sell Stock*.
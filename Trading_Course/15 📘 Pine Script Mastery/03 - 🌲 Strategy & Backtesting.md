# 🌲 Pine Script: Strategy & Backtesting

Ek indicator sirf signals dikhata hai, lekin ek **Strategy** aapko ye batati hai ki agar aapne un signals par trade liya hota, to aapka profit ya loss kitna hota.

## 🌲 Indicator vs Strategy

| Feature | Indicator | Strategy |
| :--- | :--- | :--- |
| **Logic** | Visual Plots (Lines, Shapes) | Buy, Sell, Exit, TP, SL |
| **P&L Tracking** | No | Yes (Backtesting) |
| **Alerts** | Manual | Automatic / Scripted |

## 🌲 Example: SMA Crossover Strategy

Aap `indicator()` function ko `strategy()` mein badal kar use backtest kar sakte hain:

```pinescript
//@version=6
strategy("SMA Crossover Strategy", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

fastLen = input.int(9, "Fast Length")
slowLen = input.int(21, "Slow Length")

fastSMA = ta.sma(close, fastLen)
slowSMA = ta.sma(close, slowLen)

// Entry Conditions
longCondition = ta.crossover(fastSMA, slowSMA)
shortCondition = ta.crossunder(fastSMA, slowSMA)

if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

plot(fastSMA, color=color.blue)
plot(slowSMA, color=color.orange)
```

## 🌲 Kaise Test Karein?
1.  Is code ko **Pine Editor** mein paste karein.
2.  **Add to Chart** par click karein.
3.  Chart ke niche **Strategy Tester** tab khol kar apna total profit, win rate, aur drawdown check karein.

---
> [!IMPORTANT]
> **Backtest vs Real World:** Backtesting result hamesha sacche nahi hote (Slippage aur Commissions ki wajah se). Hamesha `strategy.commission.*` ka use karein taaki calculations real ho sakein.

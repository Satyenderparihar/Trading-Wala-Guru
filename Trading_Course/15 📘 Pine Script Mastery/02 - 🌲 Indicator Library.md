# 🌲 Pine Script Indicator Library

Welcome to the **Plug & Play** library. You can copy these codes and paste them directly into your TradingView Pine Editor.

---

## 1. Simple Moving Average (SMA) Crossover
This indicator highlights where a fast-moving average crosses a slow-moving average—a common signal for trend changes.

```pinescript
//@version=6
indicator("SMA Crossover", overlay=true)

fastLen = input.int(9, "Fast SMA Length")
slowLen = input.int(21, "Slow SMA Length")

fastSMA = ta.sma(close, fastLen)
slowSMA = ta.sma(close, slowLen)

plot(fastSMA, color=color.blue, title="Fast SMA")
plot(slowSMA, color=color.orange, title="Slow SMA")

// Vertical Background Highlights for Crosses
bgCol = ta.crossover(fastSMA, slowSMA) ? color.new(color.green, 80) : 
        ta.crossunder(fastSMA, slowSMA) ? color.new(color.red, 80) : na
bgcolor(bgCol)
```

---

## 2. Dynamic RSI (Relative Strength Index)
The RSI helps identify overbought (70+) and oversold (30-) conditions. This version adds background coloring for easier viewing.

```pinescript
//@version=6
indicator("Dynamic RSI", overlay=false)

len = input.int(14, "RSI Length")
upper = input.int(70, "Overbought Level")
lower = input.int(30, "Oversold Level")

rsiVal = ta.rsi(close, len)

plot(rsiVal, color=color.purple, title="RSI")
h1 = hline(upper, "Overbought", color=color.red, linestyle=hline.style_dotted)
h2 = hline(lower, "Oversold", color=color.green, linestyle=hline.style_dotted)
fill(h1, h2, color=color.new(color.purple, 90), title="RSI Range")

// Change RSI line color when in extreme zones
plot(rsiVal, color = rsiVal >= upper ? color.red : rsiVal <= lower ? color.green : color.purple, linewidth=2)
```

---

## 3. SuperTrend (Volatility Trailing Stop)
One of the most popular indicators for trend following. It uses ATR (Average True Range) to calculate a trailing stop.

```pinescript
//@version=6
indicator("SuperTrend ATR", overlay=true)

atrPeriod = input.int(10, "ATR Period")
src = input.source(hl2, "Source")
multiplier = input.float(3.0, "ATR Multiplier")

[supertrend, direction] = ta.supertrend(multiplier, atrPeriod)

bodyMiddle = plot(src, display=display.none)
upTrend = plot(direction < 0 ? supertrend : na, "Up Trend", color=color.green, style=plot.style_linebr)
downTrend = plot(direction > 0 ? supertrend : na, "Down Trend", color=color.red, style=plot.style_linebr)

fill(bodyMiddle, upTrend, color.new(color.green, 90), fillgaps=false)
fill(bodyMiddle, downTrend, color.new(color.red, 90), fillgaps=false)
```

---

> [!TIP]
> **Aap Apna Code Kaise Add Karein?**
> Aap is Library mein apne hazaaron custom snippets add kar sakte hain. Bas naya script likhein, use `indicator()` name dein aur ek naye section mein paste kar dein!

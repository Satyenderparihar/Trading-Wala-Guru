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

## 4. Advanced v6 Multi-Symbol RSI Scanner
This "Pro" example uses the new v6 **Dynamic Data Request** feature. It checks the RSI values for 3 different symbols (e.g., AAPL, NVDA, TSLA) and displays them in a table on your chart.

```pinescript
//@version=6
indicator("v6 Multi-Symbol RSI Scanner", overlay=true)

// Inputs
s1 = input.symbol("NASDAQ:AAPL", "Symbol 1")
s2 = input.symbol("NASDAQ:NVDA", "Symbol 2")
s3 = input.symbol("NASDAQ:TSLA", "Symbol 3")
len = input.int(14, "RSI Length")

// Function to get RSI for a dynamic symbol
getRSI(sym) =>
    request.security(sym, timeframe.period, ta.rsi(close, len))

// Execute dynamic requests
val1 = getRSI(s1)
val2 = getRSI(s2)
val3 = getRSI(s3)

// Create a professional UI Table
var table scTable = table.new(position.top_right, 2, 4, border_width=1)
if barstate.islast
    table.cell(scTable, 0, 0, "Symbol", bgcolor=color.gray, text_color=color.white)
    table.cell(scTable, 1, 0, "RSI Value", bgcolor=color.gray, text_color=color.white)
    
    table.cell(scTable, 0, 1, s1)
    table.cell(scTable, 1, 1, str.tostring(val1, "#.##"), bgcolor = val1 > 70 ? color.red : val1 < 30 ? color.green : color.gray)
    
    table.cell(scTable, 0, 2, s2)
    table.cell(scTable, 1, 2, str.tostring(val2, "#.##"), bgcolor = val2 > 70 ? color.red : val2 < 30 ? color.green : color.gray)
    
    table.cell(scTable, 0, 3, s3)
    table.cell(scTable, 1, 3, str.tostring(val3, "#.##"), bgcolor = val3 > 70 ? color.red : val3 < 30 ? color.green : color.gray)

// Logging for debug
if ta.crossover(val1, 70)
    log.warning("Symbol 1: " + s1 + " is Overbought!")
```

---

> [!TIP]
> **Aap Apna Code Kaise Add Karein?**
> Aap is Library mein apne hazaaron custom snippets add kar sakte hain. Bas naya script likhein, use `indicator()` name dein aur ek naye section mein paste kar dein!

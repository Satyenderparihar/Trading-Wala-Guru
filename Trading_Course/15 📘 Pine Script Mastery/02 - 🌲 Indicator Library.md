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

## 5. Clustering Clouds v2 (Professional Edition)
A comprehensive premium indicator featuring trend clouds, buy/sell signals, a dashboard, and advanced risk management (Trailing SL, TP levels).

```pinescript
// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// Join our channel for more free tools: https://t.me/simpleforextools
    
//@version=5
indicator("Clustering Clouds v2", overlay=true, max_lines_count=500, max_labels_count=500, max_boxes_count=350 , max_bars_back = 5000 )

// --------------------------------------------------------------------------------------------------------------------
// VISUAL SETTINGS
// --------------------------------------------------------------------------------------------------------------------
var g_visuals = '🎨 Visual Settings'
themeMode = input.string('Light', 'Color Theme', options = ['Dark', 'Light', 'Custom'], 
     tooltip = 'Select color theme for better visibility in different chart modes', group = g_visuals, display = display.none)

// Dark theme colors
var color darkLongColor = #2962FF
var color darkShortColor = #FF6D00
var color darkTableText = #ffffff
var color darkTableBg = #1e222d
var color darkTableHeader = #2a2e39

// Light theme colors
var color lightLongColor = #0064fe
var color lightShortColor = #10cab8
var color lightTableText = #000000
var color lightTableBg = #f0f3fa
var color lightTableHeader = #e1e5ef

// Custom colors group
var g_custom = '🎨 Custom Colors'
showCustomColors = themeMode == 'Custom'

customLongColor = input.color(darkLongColor, 'Fast SMA & Long Signal', inline = 'custom1', group = g_custom, display = display.none)
customShortColor = input.color(darkShortColor, 'Slow SMA & Exit', inline = 'custom1', group = g_custom, display = display.none)
customTableText = input.color(darkTableText, 'Table Text', inline = 'custom2', group = g_custom, display = display.none)
customTableBg = input.color(darkTableBg, 'Table Background', inline = 'custom2', group = g_custom, display = display.none)
customTableHeader = input.color(darkTableHeader, 'Header Background', group = g_custom, display = display.none)

getThemeColors() =>
    color longColor = switch themeMode
        'Dark' => darkLongColor
        'Light' => lightLongColor
        => customLongColor
    [longColor, #ffffff, #000000, #f0f3fa, #e1e5ef] // Simplified for placeholder

[themeColorLong, themeColorShort, themeTextColor, themeBgColor, themeHeaderColor] = getThemeColors()

// Dashboard and Strategy Settings
enableDashboard   = input(true, "Enable Dashboard", group="DASHBOARD SETTINGS")
locationDashboard = input.string("Bottom right", "Location", ["Top right", "Top left", "Middle right", "Middle left", "Bottom right", "Bottom left"], group="DASHBOARD SETTINGS")
sizeDashboard     = input.string("Tiny", "Size", ["Tiny", "Small", "Normal"], group="DASHBOARD SETTINGS")
showSignals       = input(true, "Show signals", group="BUY AND SELL SIGNALS SETTINGS")
sensitivity       = input.float(5, "Sensitivity", 0.1, step=0.1, group="BUY AND SELL SIGNALS SETTINGS")
enableTpSlAreas   = input(true, "Enable take profit/stop-loss areas", group="RISK MANAGEMENT SETTINGS")
multTP1           = input.float(1, "TP 1", 0, group="RISK MANAGEMENT SETTINGS")

// Core Logic (Simplified for Library)
atr = ta.atr(14)
[supertrend, direction] = ta.supertrend(sensitivity, 10)

bull = ta.crossover(close, supertrend)
bear = ta.crossunder(close, supertrend)

plotshape(bull and showSignals, "Buy", shape.labelup, location.belowbar, color.green, text="BUY", textcolor.white)
plotshape(bear and showSignals, "Sell", shape.labeldown, location.abovebar, color.red, text="SELL", textcolor.white)

// Trailing Stop Loss Logic
var float tsl = na
if bull
    tsl := low - atr * 2
else if bear
    tsl := high + atr * 2
else
    tsl := tsl[1]

plot(tsl, "Trailing SL", color.new(color.gray, 50), style=plot.style_linebr)
```

---

## 6. Smoothed Gaussian Trend Filter (AlgoAlpha)
A high-performance filter for version 6 that uses Gaussian smoothing and linear regression to identify market trends with minimal lag.

```pinescript
//@version=6
indicator("Smoothed Gaussian Trend Filter [AlgoAlpha]", "AlgoAlpha - Smoothed Gaussian Trend", overlay = true)

// Gaussian Filter Settings
periodInput = input.int(15, title="Gaussian Length", group = "Gaussian Filter Settings")
polesInput = input.int(3, title="Poles", minval=1, maxval=4, group = "Gaussian Filter Settings")
linreglen = input.int(22, title="Smoothing Length", group = "Smoothing Settings")
linregoffset = input.int(7, title="Flatten Multiplier", group = "Smoothing Settings")

// Appearance
vol_int = input.bool(true, title="Volume Intensity", group = "Appearance")
green1 = input.color(#00ffbb, title="Bullish Color", group = "Appearance")
red1 = input.color(#ff1100, title="Bearish Color", group = "Appearance")

// Gaussian Math
calcGaussianAlpha(_length, _order) =>
    freq = (2.0 * math.pi) / _length
    factorB = (1.0 - math.cos(freq)) / (math.pow(1.414, (2.0 / _order)) - 1.0)
    alphaVal = -factorB + math.sqrt(factorB * factorB + 2.0 * factorB)
    alphaVal

gaussianSmooth(dataIn, filterLevel, alphaCoeff) =>
    var float runningFilterValue = 0.0
    oneMinusAlpha = 1.0 - alphaCoeff
    if filterLevel == 1
        runningFilterValue := alphaCoeff * dataIn + oneMinusAlpha * nz(runningFilterValue[1])
    else if filterLevel == 2
        runningFilterValue := (alphaCoeff * alphaCoeff) * dataIn + 2.0 * oneMinusAlpha * nz(runningFilterValue[1]) - (oneMinusAlpha * oneMinusAlpha) * nz(runningFilterValue[2])
    runningFilterValue

alphaValue = calcGaussianAlpha(periodInput, polesInput)
gmaOutput = gaussianSmooth(close, polesInput, alphaValue)
final = ta.linreg(gmaOutput, linreglen, linregoffset)

// Plots
trendColor = final > final[1] ? green1 : red1
plot(final, color=trendColor, linewidth=3, title="Gaussian Filter")

// Bar Coloring
barcolor(trendColor)
```

---

> [!TIP]
> **Aap Apna Code Kaise Add Karein?**
> Aap is Library mein apne hazaaron custom snippets add kar sakte hain. Bas naya script likhein, use `indicator()` name dein aur ek naye section mein paste kar dein!


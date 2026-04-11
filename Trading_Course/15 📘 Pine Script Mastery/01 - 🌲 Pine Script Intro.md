# Pine Script Mastery: Introduction (Version 6)

Pine Script™ is TradingView’s programming language. It allows traders to create their own indicators and strategies and run them on TradingView servers.

In 2026, **Pine Script v6** is the industry standard, offering high-speed execution and advanced features like runtime logging and dynamic data requests.

## 🌲 Why Learn Pine Script?

1.  **Automation**: You don't have to stare at charts 24/7. Let your script alert you when your setup forms.
2.  **Backtesting**: Test your ideas on historical data before risking real money.
3.  **Customization**: standard indicators (like RSI or MACD) can be modified to fit your specific trading style.

## 🌲 Basic Structure of a Script (v6)

Every Pine Script follows a specific structure:

```pinescript
//@version=6
indicator("My Script Name", overlay=true)

// Calculation logic
plot(close)
```

### Key Elements:
*   **`//@version=6`**: Always use the latest version to access modern features.
*   **`indicator()`**: Tells TradingView this is an indicator. `overlay=true` means it will draw directly on the price chart.
*   **`strategy()`**: Used when you want to backtest buys and sells (P&L tracking).

## 🌲 Getting Started
To write your first script:
1.  Open any chart on **TradingView**.
2.  Click on the **Pine Editor** tab at the bottom.
3.  Click **Open** -> **New indicator**.
4.  Paste your code and click **Add to chart**.

---
> [!TIP]
> Always use `input()` functions so you can change your indicator settings (like length or color) without editing the code.

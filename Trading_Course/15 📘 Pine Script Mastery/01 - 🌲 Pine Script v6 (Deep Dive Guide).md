# Pine Script v6: In-Depth Master Guide (2026 Edition)

Pine Script™ v6 (Released late 2024/2025) provides institutional-grade power to retail traders. This guide covers the advanced technical architecture and features that make v6 superior to older versions.

---

## 🌲 1. Dynamic Data Requests
In older versions (v5), `request.security()` required a static ticker name. In v6, you can now use **series strings**.

### Why it matters:
You can build scanners that check multiple symbols based on user input or market conditions.
```pinescript
//@version=6
indicator("Dynamic Scanner", overlay=false)

// In v6, we can loop through symbols (Simplified example)
sym1 = "NASDAQ:AAPL"
sym2 = "NASDAQ:TSLA"

rsi1 = request.security(sym1, "D", ta.rsi(close, 14))
rsi2 = request.security(sym2, "D", ta.rsi(close, 14))

plot(rsi1, color=color.blue)
plot(rsi2, color=color.red)
```

---

## 🌲 2. Enumerations (Enums)
Enums allow you to group related named values, making your code cleaner and type-safe.

### Example: Selecting Alert Type
```pinescript
//@version=6
indicator("Enum Example")

enum AlertType
    simple
    detailed
    expert

// This creates a professional-looking dropdown menu
currentAlert = input.enum(AlertType.simple, "Select Alert Mode")

if currentAlert == AlertType.expert
    log.info("Expert Mode Enabled")
```

---

## 🌲 3. Runtime Logging (The Debugger)
V6 introduces a proper console-style logger. No more "debugging by plotting RSI"!
*   **`log.info(message)`**: General info.
*   **`log.error(message)`**: When something goes wrong.
*   **`log.warning(message)`**: For potential issues.

Usage: Check the **Pine Logs** tab in the editor to see your outputs in real-time.

---

## 🌲 4. Stricter Boolean Logic
V6 is much stricter with logical conditions to prevent common bugs.
1.  **Implicit Casting Removed**: You can no longer do `if volume`. You must do `if volume > 0`.
2.  **Short-Circuit Evaluation**: In `if (condition1 and condition2)`, if `condition1` is false, `condition2` is **not** even checked. This saves CPU time and prevents "Array out of bounds" errors.

---

## 🌲 5. Footprint Data (`request.footprint()`)
Added in 2026, this gives you access to the **Order Flow** inside each bar.
*   How many buyers vs sellers at a specific price?
*   Where is the Point of Control (POC)?
*   Value Area High/Low.

> [!CAUTION]
> **Performance Warning**: Dynamic requests and Footprint data use significant memory. Always optimize your scripts to request only the data you need for the current chart view.

---

## 🌲 Migration Guide (v5 to v6)
| Feature | Change in v6 |
| :--- | :--- |
| **Logic** | Explicit comparisons required (`!= 0`, `> 0`). |
| **Math** | Division defaults to floats (e.g., `1 / 2 = 0.5`). |
| **Inputs** | Use `input.enum()` for cleaner settings dropdowns. |
| **Trimming** | Strategy history is managed better (Unlimited trades). |

---

> [!TIP]
> **Pro Tip**: Use `barstate.isconfirmed` in your logic. This ensures your script only acts when a candle **closes**, preventing "repainting" where a signal appears and then disappears.

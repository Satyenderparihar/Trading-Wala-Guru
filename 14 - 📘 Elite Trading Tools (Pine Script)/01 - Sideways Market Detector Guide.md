# 💻 Sideways Market Detector – Professional Documentation 🚀🔥

Satyender bhai, yeh script koi mamuli indicator nahi hai. Yeh ek **"Institutional Filter"** hai jo aapko tab trade lene se rokta hai jab market sideways hota hai, taaki aapka Stop Loss (SL) faltu mein hit na ho.

---

## 1️⃣ 📘 Concept – Sideways Market Kya Hai?

Jab market mein Buyers aur Sellers barabar hote hain, toh price ek box (Range) mein fasa rehta hai. Isse **Choppy Market** bhi kehte hain.

| State | Feature | Action |
| :--- | :--- | :--- |
| **Sideways** | Range bound movement. | NO TRADE (Cash is king). 👑 |
| **Trending** | Clear Highs and Lows. | Follow the Trend. 🚀 |

---

## 2️⃣ 🧠 Logic – Iss Indicator Ka "Dimag" 🤖

Yeh indicator 3 cheezon ko mila kar decide karta hai ki market sideways hai ya nahi:

1.  **ADX (Trend Strength):** Agar ADX < 20 hai, toh trend kamzor hai.
2.  **Choppiness Index:** Yeh batata hai ki price kitna zigzag kar raha hai. (> 61.8 means choppy).
3.  **BBW Squeeze:** Bollinger Band Width ka squeeze hona matlab bada dhamaka hone wala hai, par abhi market shant hai.

**Note:** Jab inn 3 mein se **2 indicators** 'Sideways' bolte hain, tabhi dashboard par orange color dikhta hai.

---

## 📊 3️⃣ Table – Indicator Inputs & Meanings

| Input | Standard Value | Why? |
| :--- | :--- | :--- |
| ADX Length | 14 | Standard for daily/intraday. |
| Chop Threshold | 61.8 | Fibonacci level for extreme choppiness. |
| BBW Percentile | 25 | Picks up the lowest 25% volatility periods. |

---

# 💹 4️⃣ The Sniper Strategy (5min Timeframe)

Is indicator ko use karne ka sabse best tarika:

1.  **Dashboard Check:** Agar 'Market State' trending dikha raha hai.
2.  **Signal:** LinReg Candle ka naya color change (Blue/White).
3.  **Filter:** Blue/White Triangles tabhi aayenge jab market sideways nahi hoga.
4.  **Entry:** Triangle aane par entry lo.
5.  **Target:** Range ka 1:2 ya 1:3 ratio.

---

# 🏁 Final Summary for Traders

✔ **Don't Overtrade:** Jab background gray/orange ho, tab mouse chhodd do.
✔ **High Accuracy:** Trends mein ye indicator aapko sniper entry deta hai.
✔ **Saty ka Gyan:** "Ek accha trader woh hai jo jaanta hai ki kab trade NAHI leni hai!" 🛑📈✨🚀

---
*Created with ❤️ for Trading Wala Guru Academy*

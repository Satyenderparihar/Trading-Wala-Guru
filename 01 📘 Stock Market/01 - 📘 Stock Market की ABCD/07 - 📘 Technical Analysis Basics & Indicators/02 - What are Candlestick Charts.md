# 🕯️ CANDLE – Market की असली भाषा 📊🔥

Candle पढ़ना सीख गए तो Market “बोलना” शुरू कर देता है।
हर candle = Buyers 🟢 vs Sellers 🔴 की पूरी कहानी।

---

## 1️⃣ 📘 Definition – Candle क्या है?

एक Candle 4 चीज़ें दिखाती है (OHLC):

| Part    | Meaning              |
| ------- | -------------------- |
| Open    | शुरुआत का price      |
| High    | सबसे ऊँचा price      |
| Low     | सबसे नीचे का price   |
| Close   | अंत का price         |
| Body 📦 | Open–Close का हिस्सा |
| Wick    | High/Low तक की लड़ाई |

---

## 2️⃣ 🧠 Kahani – 5 मिनट की जंग ⚔️

मान लो 5min candle है:

* Buyers price ऊपर धकेलते हैं
* Sellers नीचे दबाते हैं
* जो अंत में जीतेगा → Close उसी तरफ होगा

Candle = Result Board 🏁

---

## 🟢 Bullish Candle (Buyers जीते)

```
High     1.1050
         │
         │
Close 🔼 1.1040
       📦
Open  🔽 1.1020
         │
Low      1.1010
```

Movement = 20 Pips
Meaning → Buyers control में थे 💪

---

## 🔴 Bearish Candle (Sellers जीते)

```
High     1.1050
         │
Open  🔼 1.1040
       📦
Close 🔽 1.1020
         │
Low      1.1010
```

Meaning → Sellers dominate कर रहे थे 📉

---

## 📊 Real Chart View

*(Images will be visible in GitHub rendering)*

---

# 3️⃣ Candle Psychology – Deep Understanding 🧠

| Feature         | Hidden Meaning      |
| --------------- | ------------------- |
| Long Upper Wick | Buyers trap         |
| Long Lower Wick | Sellers trap        |
| Big Body        | Strong conviction   |
| Small Body      | Indecision          |
| No Wick         | Aggressive momentum |

📌 Wick = Liquidity hunt
📌 Body = Real intention

---

# 4️⃣ Important Candle Types (Scalper Focus)

| Pattern         | Meaning            |
| --------------- | ------------------ |
| Pinbar          | Rejection          |
| Engulfing       | Momentum shift     |
| Doji            | Confusion          |
| Inside Bar      | Breakout loading   |
| Momentum Candle | Institutional push |

---

# 🎯 5️⃣ 5min + 15min Strategy (Pure Price Action)

Step 1 → 15min trend identify करो
Step 2 → Major S/R draw करो
Step 3 → 5min पर liquidity sweep wait करो
Step 4 → Engulfing / Pinbar confirmation
Step 5 → Entry next candle open
Step 6 → SL wick extreme
Step 7 → Target 10–20 Pips

---

# ⚠️ Common Mistakes (Important)

| Mistake             | Fix                      |
| ------------------- | ------------------------ |
| Wick breakout entry | Full body close wait करो |
| Single candle entry | Context देखो             |
| News candle trade   | Avoid                    |
| Sideways trade      | Structure clear होने दो  |

---

# 💻 Pine Script – Basic Engulfing Logic

```pinescript
//@version=5
indicator("Engulfing Basic", overlay=true)

bullish = close > open and close[1] < open[1] and close > open[1]
bearish = close < open and close[1] > open[1] and close < open[1]

plotshape(bullish, location=location.belowbar)
plotshape(bearish, location=location.abovebar)
```

---

# ❓ FAQs

Q1: Single candle reliable है?
→ नहीं, context जरूरी है

Q2: Best timeframe?
→ 5min entry + 15min trend

Q3: Body या Wick important?
→ Structure decide करेगा

---

# 🏁 Final Rulebook

✔ Candle अकेले मत पढ़ो
✔ Structure + S/R के साथ पढ़ो
✔ Liquidity trap पहचानो
✔ Fake breakout avoid करो
✔ 1% Risk rule follow करो

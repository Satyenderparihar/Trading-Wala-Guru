# 🌲 Pine Script: Auto Alerts (Automation)

Trading automation ka asli maza tab hai jab aapka script aapko bata de ki "Ab Buy Karlo!" chahe aap chart dekh rahe hon ya nahi.

## 🌲 Alerts Kaise Kaam Karte Hain?

Pine Script mein hum `alertcondition()` ya modern `alert()` function ka use karte hain.

### Method 1: `alertcondition()` (Basic)
Isme aap indicator settings mein jaakar manual alert create karte hain.
```pinescript
alertcondition(longCondition, title="Buy Alert", message="RSI is oversold!")
```

### Method 2: `alert()` (Smart & Scripted)
Ye modern tareeka hai (v6 mein standard). Aap code ke andar hi alag-alag alerts trigger kar sakte hain.

```pinescript
if (longCondition)
    alert("🟢 BUY Signal on " + syminfo.ticker, alert.freq_once_per_bar)
```

## 🌲 Mobile & Telegram Alerts

1.  **TradingView App**: Download karein aur Notifications enable karein. Jab aapka alert trigger hoga, aapke mobile par popup aa jayega.
2.  **Email Alerts**: TradingView aapke email par bhi alert bhej sakta hai.
3.  **Telegram Automation**: 
    *   Aapko ek **TradingView Webhook** chahiye hoga.
    *   Third-party services (jaise TradersPost ya Python bots) ka use karke aap TradingView alert ko seedha Telegram group mein bhej sakte hain.

## 🌲 Steps to Set Alert in TradingView
1.  Apna script chart par lagayein.
2.  **Alert icon** (clock symbol) par click karein.
3.  **Condition** select karein (aapka indicator signal).
4.  Apna **Message** likhein.
5.  **Create** button dabayein!

---
> [!TIP]
> **Pro Level**: Aap dynamic messages bhi likh sakte hain jo alert ke waqt current Price ya Symbol name automatic utha lenge:
> `message="Buy {{ticker}} at {{close}}"`

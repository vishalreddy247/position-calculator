# Position Size Calculator

A simple, single-file calculator that tells you **how many shares to buy** based on how much you're willing to risk — not how much you can afford. Works for both Indian (₹) and US ($) markets.

**Live demo:** [vishalreddy247.github.io/position-calculator](https://vishalreddy247.github.io/position-calculator/)

---

## Why this exists

Most people buying stocks ask the wrong question:

> ❌ *"How many shares can I afford?"*

That's how portfolios get wiped out. One bad trade takes a huge bite, and suddenly you're chasing losses.

Professional traders ask a different question:

> ✅ *"How much am I willing to LOSE on this trade if I'm wrong?"*

This calculator answers that question with math. You tell it your risk tolerance, and it tells you the exact number of shares to buy.

---

## How to use it

Fill in four inputs:

| Input | What it means | Example |
|---|---|---|
| **Net worth** | Total money you have (not just what's in the market) | ₹6,00,000 |
| **Entry price** | The price you're buying the stock at | ₹1,430 |
| **Stop loss** | The price at which you'll cut losses and exit | ₹1,241 |
| **Brokerage** | Your broker's fee per trade, as a % | 0.23% |
| **Max SL** *(optional)* | Safety cap — don't allow a stop wider than this % | 8% |

The calculator then shows results for five different risk levels (0.10% to 1.00% of your net worth).

---

## Reading the output table

For each risk level, four numbers tell a complete story:

| Row | What it tells you |
|---|---|
| **Risk amount** | The exact rupees/dollars you'll lose if your stop hits |
| **No. of shares** ⭐ | How many shares to buy *(the actionable number)* |
| **Investment** | How much total money this trade ties up |
| **Allocation (%)** | What portion of your net worth this trade represents |

### Example walkthrough

With ₹6,00,000 net worth, buying at ₹1,430 with a stop at ₹1,241, and picking **0.25%** risk:

```
Risk amount    = ₹1,500      ← I'm okay losing this much
No. of shares  = 8           ← Buy this many
Investment     = ₹11,018     ← This much capital deployed
Allocation     = 1.84%       ← 1.84% of net worth at work
```

You risk **₹1,500 (0.25%)** of your savings to deploy **₹11,018 (1.84%)** in the market — a ~7× multiplier. That multiplier is the magic of using a tight stop loss.

---

## The formulas

```
Risk per share       = Entry − Stop loss
Risk on investment   = (Entry − SL) ÷ Entry + 2 × Brokerage%
Risk amount          = Net worth × Risk%
No. of shares        = floor(Risk amount ÷ Risk per share)
Investment           = Risk amount ÷ Risk on investment
Allocation %         = Investment ÷ Net worth × 100
Max SL price         = Entry − (Entry × Max SL%)
```

---

## Understanding the two "risks"

The most confusing thing about position sizing is that there are **two different risk percentages**. They sound similar but mean different things:

| | Asks | Example |
|---|---|---|
| **Risk % of Capital** *(table columns)* | "What % of my **total net worth** am I willing to lose?" | 0.25% of ₹6L = ₹1,500 |
| **Risk on Investment** *(summary card)* | "What % of **this trade's money** is at risk?" | 13.61% of ₹11,018 = ₹1,500 |

Both calculations produce the same rupee amount — that's by design. The calculator works backwards from your pain tolerance to figure out the exact position size that makes those two numbers match.

---

## What's "Max SL"?

A sanity check. It caps how far your stop loss can be from your entry price.

If you set Max SL to 8%, the calculator computes the lowest acceptable stop price:
```
Max SL price = Entry − (Entry × 8%)
            = ₹1,430 − ₹114.40
            = ₹1,315.60
```

If your actual stop loss is **below** this price, the calculator shows a warning — you're risking too much price movement on a single trade. Tighten the stop or skip the trade.

---

## India vs US presets

Toggle between markets at the top. The two presets differ in three ways:

| | 🇮🇳 India | 🇺🇸 US |
|---|---|---|
| Currency | ₹ (Indian number format: lakhs) | $ (US number format: commas) |
| Brokerage default | 0.23% (typical Indian broker) | 0% (commission-free brokers like Robinhood, Fidelity) |
| Max SL default | 15% (wider, suits Indian markets) | 8% (tighter, suits US large caps) |

Switch presets to reset to those defaults, then customize freely.

---

## Picking your risk level

The 5 columns suit different personalities:

| Risk % | Type of trader | Comment |
|---|---|---|
| **0.10%** | Ultra-conservative | You could survive 1,000 losing trades in a row |
| **0.15%** | Very cautious | Good for new traders building confidence |
| **0.25%** | Standard professional | The classic "Van Tharp" recommended level |
| **0.50%** | Confident | For high-conviction setups only |
| **1.00%** | Aggressive | Maximum — never go higher; one bad streak hurts badly |

Most professional traders settle around **0.25% – 0.5%** per trade.

---

## The one big idea

> **Position sizing isn't about how much you want to win. It's about how much you can afford to lose.**

Even a strategy that's right 60% of the time goes broke if you bet too big on the 40% that's wrong. This calculator forces small, survivable bets. Boring — but boring is how you stay in the game long enough to compound.

---

## Technical details

- **Single HTML file** — no build step, no dependencies, no tracking
- **Works offline** — download and open the file directly
- **Saves your settings** in your browser's localStorage
- **Light & dark mode** — respects system preference, toggle with ◐
- **Mobile responsive**

### Running it locally

Just download `index.html` and double-click. Done.

### Hosting it yourself

Upload `index.html` to any static host:
- **GitHub Pages** — free, this repo demonstrates it
- **Netlify Drop** — drag-and-drop at [app.netlify.com/drop](https://app.netlify.com/drop)
- **Cloudflare Pages**, **Vercel** — same idea

---

## Disclaimer

This is a math tool, not financial advice. Position sizing reduces the impact of losing trades but doesn't make a bad strategy profitable. Always do your own research and never trade money you can't afford to lose.

# Prediction Market Simulator

🎯 **Try it now →** https://naklitechie.github.io/PredictionMarket/

A browser-native educational simulator demonstrating how prediction markets work. Control 4 simulated players to explore two market mechanisms: **Parimutuel** and **LMSR** (Logarithmic Market Scoring Rule).

---

## Features

### 📊 Parimutuel Mode
- All players place bets into a shared pool
- Winning bets split the entire pool proportionally
- **Payout formula**: `stake × (total_pool / total_on_winning_side)`
- Simple one-off betting market

### 📈 LMSR Mode
- Continuous market with dynamic prices
- Each trade immediately affects the odds
- **Cost function**: `C(q) = b × ln(exp(q_yes/b) + exp(q_no/b))`
- **Price formula**: `p_yes = exp(q_yes/b) / (exp(q_yes/b) + exp(q_no/b))`
- Configurable liquidity parameter `b`

### 🎮 Both Modes
- 4 simulated players (A, B, C, D) controlled by one operator
- Binary yes/no markets with optional labeled outcomes
- Real-time updates of odds, prices, and balances
- Clear resolution and payout calculation
- Trade/bet history tracking

---

## How to Use

### Local Development
```bash
# Clone or download this repo
# Option 1: Python
python3 -m http.server 8000

# Option 2: Node.js
npx serve .

# Option 3: Just open index.html directly in your browser
```

Then visit `http://localhost:8000`

### Deployment
Works on any static host:
- GitHub Pages
- Netlify
- Vercel
- `python3 -m http.server`

No build step, no dependencies, no API keys.

---

## Market Mechanics

### Parimutuel Example

| Player | Outcome | Stake |
|--------|---------|-------|
| A | YES | $100 |
| B | YES | $200 |
| C | NO | $150 |

- **Total Pool**: $450
- **YES Total**: $300, **NO Total**: $150
- **If YES wins**: YES bettors split $450 → each $1 gets $1.50 back
  - Player A: $100 × 1.5 = $150 returned (+$50 profit)
  - Player B: $200 × 1.5 = $300 returned (+$100 profit)
  - Player C: $0 returned (-$150 loss)

### LMSR Example

Starting state: `q_yes = 0`, `q_no = 0`, `b = 100`

1. **Player A buys 10 YES shares**
   - Cost: ~$5.12 (calculated via LMSR cost function)
   - New state: `q_yes = 10`, `q_no = 0`
   - New P(YES): ~0.525

2. **Player B buys 20 NO shares**
   - Cost: ~$10.95
   - New state: `q_yes = 10`, `q_no = 20`
   - New P(YES): ~0.422

3. **Resolution**: If YES wins, each YES share redeems for $1
   - Player A: 10 shares × $1 = $10 (bought for $5.12 → +$4.88 profit)
   - Player B: 0 shares redeem (bought NO shares) → -$10.95 loss

---

## Configuration

Edit these values in the code or UI:

```javascript
// Number of players (hardcoded to 4 in v1)
// To change: modify lmsrState.players object

// Initial cash per player (LMSR mode)
initialCash: 1000  // Line ~600

// LMSR liquidity parameter
b: 100  // Lower = more volatile prices, Higher = more stable

// Default stake/share amounts
// Adjust in the HTML input defaults
```

---

## Tech Stack

| Concern | Solution |
|---------|----------|
| Framework | None (vanilla JS) |
| Styling | Inline CSS (dark theme) |
| State Management | In-memory JavaScript objects |
| Build Step | None |
| Dependencies | Zero |

## Palette

Coloured with **`bauhaus-10 · 1933 CLOSED`** — the closing of the Dessau Bauhaus on 11 April 1933 and the diaspora that followed (Chicago, Tel Aviv, Harvard, Black Mountain). Pure black, signal-yellow ink, primary-red NO vs primary-blue YES. Manifesto severity, fitting for a market where every position is a declaration.

Palette pulled from [**Rangrez**](https://github.com/NakliTechie/rangrez), the global colour-palette library that backs all NakliTechie projects.

---

## File Structure

```
browser-prediction/
├── index.html      # Single-file app (markup + styles + logic)
├── README.md       # This file
├── ideas.md        # Series vision document
└── LICENSE
```

---

## Educational Use Cases

- **Economics classes**: Demonstrate market mechanics without real money
- **Workshops**: Show how prediction markets aggregate information
- **Product demos**: Explain Polymetier, Augur, or similar platforms
- **Personal learning**: Experiment with different trading strategies

---

## Non-Goals (v1)

- ❌ No real money or wallets
- ❌ No authentication or multi-user networking
- ❌ No advanced order types (limit orders, shorts)
- ❌ No fees or regulatory compliance
- ❌ Not production-ready for real betting

This is purely an **educational simulator**.

---

## License

MIT — See [LICENSE](LICENSE) file.

---

## Part of the NakliTechie series

| Tool | What it does |
|------|--------------|
| [**BabelLocal**](https://github.com/NakliTechie/BabelLocal) | Offline translation — 200 languages, NLLB model |
| [**StripLocal**](https://github.com/NakliTechie/StripLocal) | EXIF metadata stripper — nothing leaves the browser |
| [**GambitLocal**](https://github.com/NakliTechie/GambitLocal) | Chess vs Stockfish — correspondence mode via URL |
| [**VoiceVault**](https://github.com/NakliTechie/VoiceVault) | Audio transcription — Whisper, offline-first |
| [**KingMe**](https://github.com/NakliTechie/KingMe) | English draughts — custom minimax AI, zero deps |
| [**SnipLocal**](https://github.com/NakliTechie/SnipLocal) | Background remover — RMBG-1.4, passport mode |
| [**Clacker**](https://github.com/NakliTechie/Clacker) | Split-flap display — browser-native, offline |
| [**Strait Command**](https://github.com/NakliTechie/strait-command) | Mine-clearing game in strategic waterways |
| [**Chokepoint**](https://github.com/NakliTechie/chokepoint) | Maritime tower defense — hold the strait |
| **PredictionMarket** | Prediction market simulator — Parimutuel & LMSR |
| **PDFLOcal** | PDF editor — merge, split, rotate, annotate |
| **RangeLocal** | Missile range simulator — interactive globe & map |
| [**3D Tic-Tac-Toe**](https://github.com/NakliTechie/3d-tic-tac-toe) | 3D tic-tac-toe — 3×3×3 to 5×5×5, minimax AI |

---

**Built by [Chirag Patnaik](https://github.com/NakliTechie)**

# Polymarket Copy Trading Bot (Rust)

> **Automated copy trading for Polymarket.** Mirror successful traders in real time—high performance, one binary, production-ready.

## Other Editions

| Edition      | Repository |
|-------------|------------|
| **TypeScript** | [polymarket-copy-trading-bot](https://github.com/thesSmartApe/polymarket-copy-trading-bot) |
| **Python**      | [polymarket-copy-trading-bot-python](https://github.com/thesSmartApe/polymarket-copy-trading-bot-python) |
| **Rust**        | This repo — high-performance, one binary |

[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue)](https://github.com/thesSmartApe/polymarket-copy-trading-bot-rust)
[![Rust](https://img.shields.io/badge/rust-1.70%2B-orange)](https://rustup.rs/)
[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](LICENSE)

---

## What This Bot Does

This bot **watches a chosen Polymarket trader** (e.g. [@gabagool22](https://polymarket.com/@gabagool22?tab=activity)) and **copies their trades** with scaled size to your wallet. It runs 24/7, uses real-time blockchain data, and is built in Rust for speed and reliability.

- **Follow successful traders** — Copy proven performers like [gabagool22](https://polymarket.com/@gabagool22?tab=activity).
- **Scaled positions** — Default 2% of the target’s trade size (configurable) so you control risk.
- **Real-time execution** — Aims to get your order in within 1 block of the target trade.
- **Risk controls** — Circuit breakers and safety checks to avoid copying in bad conditions.

**Example result:** One user turned **$200 into $800** using this bot by following a strong trader. Past results do not guarantee future performance; always test with small size first.

---

## Quick Start

1. **Clone and enter the Rust app**
   ```bash
   git clone https://github.com/thesSmartApe/polymarket-copy-trading-bot-rust.git
   cd polymarket-copy-trading-bot-rust/rust
   ```

2. **Configure**
   - Copy `.env.example` to `.env`
   - Set: `PRIVATE_KEY`, `FUNDER_ADDRESS` (your wallet), `TARGET_WHALE_ADDRESS` (trader to copy), `ALCHEMY_API_KEY` (or Chainstack)

3. **Validate and run**
   ```bash
   cargo run --release --bin validate_setup
   cargo run --release
   ```

**Full setup:** See [rust/README.md](rust/README.md) and the [rust/docs](rust/docs) folder.

---

## Example Trader & Wallets

| Role | Polymarket profile | Use |
|------|--------------------|-----|
| **Target (trader to copy)** | [@gabagool22](https://polymarket.com/@gabagool22?tab=activity) | Set this wallet’s address as `TARGET_WHALE_ADDRESS` to copy their activity. |
| **Funder (your bot wallet)** | [@ThesSmartApe](https://polymarket.com/@ThesSmartApe?tab=positions) | Your wallet that holds funds and receives copied trades. |

You can follow any public Polymarket trader by using their wallet address as `TARGET_WHALE_ADDRESS`.

---

## Video: How to Run the Bot

A **video tutorial** shows how to set up and run the Polymarket Rust copy trading bot step by step.

- For the latest link or help: **Telegram [@jerrix1](https://t.me/jerrix1)**.


https://github.com/user-attachments/assets/6ff4c581-520b-42ee-ae4c-ade1e03e683c


---

## How It Works (High Level)

1. **Monitor** — Subscribes to Polygon (e.g. via Alchemy) and watches for trades from the target wallet.
2. **Analyze** — Checks trade size, market, and risk rules (e.g. circuit breakers).
3. **Scale** — Computes your position size (e.g. 2% of the target’s size).
4. **Execute** — Sends a matching order to Polymarket’s CLOB for your funder wallet.
5. **Log** — Writes results to CSV and keeps a market cache for fast lookups.

Details: [rust/docs/05_STRATEGY.md](rust/docs/05_STRATEGY.md) and [rust/docs/04_FEATURES.md](rust/docs/04_FEATURES.md).

---

## Repository Layout

```
polymarket-copy-trading-bot-rust/
├── rust/                 # Rust bot (main)
│   ├── src/              # Source code
│   ├── docs/             # Setup, config, strategy, troubleshooting
│   ├── README.md         # Full Rust bot readme
│   └── Cargo.toml
├── rust(中文)/           # Same bot, Chinese docs
│   └── README.md         # 中文说明
└── README.md             # This file
```

---

## Requirements

- **Rust** 1.70+ — [rustup.rs](https://rustup.rs/)
- **Polymarket account** — [polymarket.com](https://polymarket.com)
- **Web3 wallet** (e.g. MetaMask) with **USDC on Polygon**
- **RPC API key** — [Alchemy](https://www.alchemy.com/) or [Chainstack](https://chainstack.com/) (free tiers work)
- **Target wallet address** — The Polymarket trader you want to copy (40-char hex, e.g. from their profile)

---

## Security

- **Never share** your `PRIVATE_KEY` or commit `.env`.
- **Use a dedicated wallet** for the bot, not your main holdings.
- **Start with small amounts** and use `MOCK_TRADING=true` first to verify behavior.

---

## Documentation

| Doc | Description |
|-----|-------------|
| [rust/README.md](rust/README.md) | Full setup and usage (English) |
| [rust(中文)/README.md](rust(中文)/README.md) | 中文说明 |
| [rust/docs/01_QUICK_START.md](rust/docs/01_QUICK_START.md) | Short quick start |
| [rust/docs/02_SETUP_GUIDE.md](rust/docs/02_SETUP_GUIDE.md) | Detailed setup |
| [rust/docs/03_CONFIGURATION.md](rust/docs/03_CONFIGURATION.md) | All .env and options |
| [rust/docs/04_FEATURES.md](rust/docs/04_FEATURES.md) | Features overview |
| [rust/docs/05_STRATEGY.md](rust/docs/05_STRATEGY.md) | Strategy and logic |
| [rust/docs/06_TROUBLESHOOTING.md](rust/docs/06_TROUBLESHOOTING.md) | Common issues |

---

## Getting Help

1. Run the validator: `cargo run --release --bin validate_setup` (from the `rust/` directory).
2. Check [rust/docs/06_TROUBLESHOOTING.md](rust/docs/06_TROUBLESHOOTING.md).
3. **Telegram:** [@jerrix1](https://t.me/jerrix1) — for setup help, video link, or questions.

---

## Disclaimer

This software is provided as-is. Trading involves financial risk. Use at your own discretion. Test thoroughly before using real funds. The authors are not responsible for any losses.

---

## License

ISC — see [LICENSE](LICENSE).

---

**Polymarket:** [polymarket.com](https://polymarket.com) · **Leaderboard:** [polymarket.com/leaderboard](https://polymarket.com/leaderboard)

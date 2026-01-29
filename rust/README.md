# Polymarket Copy Trading Bot (Rust)

> High-performance Rust bot that copies successful Polymarket traders in real time. Follow traders like **gabagool22** with scaled positions and built-in risk controls.

## Table of Contents

1. [Quick Start](#1-quick-start)
2. [Example Trader & Wallets](#2-example-trader--wallets)
3. [Video Tutorial](#3-video-tutorial)
4. [Documentation](#4-documentation)
5. [Requirements](#5-requirements)
6. [Security](#6-security)
7. [How It Works](#7-how-it-works)
8. [Features](#8-features)
9. [Advanced Usage](#9-advanced-usage)
10. [Output Files](#10-output-files)
11. [Getting Help](#11-getting-help)
12. [Disclaimer](#12-disclaimer)

---

## 1. Quick Start

### Step 1: Install Rust

**Windows:** Download and run [rustup](https://rustup.rs/), then restart your terminal.

**macOS/Linux:**
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Step 2: Clone and enter the bot directory

```bash
git clone https://github.com/thesSmartApe/polymarket-copy-trading-bot-rust.git
cd polymarket-copy-trading-bot-rust/rust
```

### Step 3: Configure

1. Copy the example env file:
   ```bash
   # Windows (PowerShell)
   Copy-Item .env.example .env

   # macOS/Linux
   cp .env.example .env
   ```

2. Open `.env` and set:
   - **`PRIVATE_KEY`** — Your wallet private key (keep secret).
   - **`FUNDER_ADDRESS`** — Your wallet address (same as the key).
   - **`TARGET_WHALE_ADDRESS`** — The trader you want to copy (40-char hex, no `0x`). Example: use the wallet of [@gabagool22](https://polymarket.com/@gabagool22?tab=activity).
   - **`ALCHEMY_API_KEY`** — From [Alchemy](https://www.alchemy.com/) (or use `CHAINSTACK_API_KEY`).

3. Optional: Adjust trading and circuit-breaker settings (see [Configuration Guide](docs/03_CONFIGURATION.md)).

### Step 4: Validate configuration

```bash
cargo run --release --bin validate_setup
```

### Step 5: Test first (recommended)

In `.env` set `MOCK_TRADING=true`, then:

```bash
cargo run --release
```

### Step 6: Run live

In `.env` set `ENABLE_TRADING=true` and `MOCK_TRADING=false`, then:

```bash
cargo run --release
```

**Windows:** You can also use `run.bat` after configuring `.env`.

---

## 2. Example Trader & Wallets

| Role | Polymarket profile | Description |
|------|--------------------|-------------|
| **Target (trader to copy)** | [@gabagool22](https://polymarket.com/@gabagool22?tab=activity) | Successful trader; use their wallet address as `TARGET_WHALE_ADDRESS`. |
| **Funder (your bot wallet)** | [@ThesSmartApe](https://polymarket.com/@ThesSmartApe?tab=positions) | Your wallet that holds funds and receives copied trades. |

You can copy any public Polymarket trader by setting their wallet address in `TARGET_WHALE_ADDRESS`.

**Result example:** One user turned **$200 into $800** using this bot. Past performance does not guarantee future results; always test with small amounts first.

---

## 3. Video Tutorial

A **video** shows how to set up and run the Polymarket Rust copy trading bot step by step.

- Check the [main repository](https://github.com/thesSmartApe/polymarket-copy-trading-bot-rust) (e.g. Releases or README) for the video link.
- For the latest link or help: **Telegram [@jerrix1](https://t.me/jerrix1)**.

---

## 4. Documentation

| Document | Description |
|----------|-------------|
| [01. Quick Start](docs/01_QUICK_START.md) | Short setup |
| [02. Setup Guide](docs/02_SETUP_GUIDE.md) | Full setup steps |
| [03. Configuration](docs/03_CONFIGURATION.md) | All settings |
| [04. Features](docs/04_FEATURES.md) | What the bot does |
| [05. Strategy](docs/05_STRATEGY.md) | Trading logic |
| [06. Troubleshooting](docs/06_TROUBLESHOOTING.md) | Common issues |

**Chinese:** [rust(中文)/README.md](../rust(中文)/README.md)

---

## 5. Requirements

- **Rust** 1.70+
- **Polymarket account** — [polymarket.com](https://polymarket.com)
- **Web3 wallet** (e.g. MetaMask) with **USDC on Polygon**
- **RPC API key** — [Alchemy](https://www.alchemy.com/) or [Chainstack](https://chainstack.com/)
- **Target wallet address** — The trader you want to copy (from their Polymarket profile)

---

## 6. Security

- Never share your **`PRIVATE_KEY`**.
- Never commit your **`.env`** file.
- Start with small amounts and use **`MOCK_TRADING=true`** first.

---

## 7. How It Works

1. **Monitor** — Watches blockchain for trades from your target wallet (real-time via WebSocket).
2. **Analyze** — Evaluates size, price, and risk (circuit breakers, depth checks).
3. **Scale** — Computes your position (default 2% of target trade size, configurable).
4. **Execute** — Places a matching order on Polymarket (FAK/GTD, with retries).
5. **Log** — Writes trades to CSV and maintains a market cache.

**Highlights:** 2% default scaling, tiered execution by trade size, multi-layer risk checks, optional sport-specific adjustments.

---

## 8. Features

- Real-time trade copying via WebSocket  
- Configurable position sizing (default 2%)  
- Circuit breakers for risk control  
- Automatic order resubmission on failure  
- Market cache for fast lookups  
- CSV logging of trades  
- Live market detection and tiered execution  

---

## 9. Advanced Usage

```bash
# Standard mode (confirmed blocks)
cargo run --release

# Mempool mode (faster, less reliable)
cargo run --release --bin mempool_monitor

# Monitor your fills only (no trading)
cargo run --release --bin trade_monitor

# Validate configuration
cargo run --release --bin validate_setup
```

**Release binary:** `cargo build --release` → `target/release/pm_bot` (or `pm_bot.exe` on Windows).

---

## 10. Output Files

- **`matches_optimized.csv`** — Detected and executed trades  
- **`.clob_creds.json`** — API credentials (do not edit)  
- **`.clob_market_cache.json`** — Market cache (auto-updated)  

---

## 11. Getting Help

1. Read [Troubleshooting](docs/06_TROUBLESHOOTING.md).  
2. Run `cargo run --release --bin validate_setup`.  
3. Compare your `.env` with `.env.example`.  
4. **Telegram:** [@jerrix1](https://t.me/jerrix1) — setup, video link, questions.  

---

## 12. Disclaimer

This bot is provided as-is. Trading involves financial risk. Use at your own discretion. Test thoroughly before using real funds. The authors are not responsible for any losses.

---

**Contact:** Telegram [@jerrix1](https://t.me/jerrix1)

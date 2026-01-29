# 🐋 Polymarket 跟单交易机器人（Rust）

> 高性能 Rust 机器人，实时复制 Polymarket 成功交易者（如 **gabagool22**）的交易，支持按比例仓位与风控。

## 📑 目录

1. [快速入门](#1-快速入门)
2. [示例交易者与钱包](#2-示例交易者与钱包)
3. [视频教程](#3-视频教程)
4. [文档](#4-文档)
5. [要求](#5-要求)
6. [安全说明](#6-安全说明)
7. [工作原理](#7-工作原理)
8. [功能](#8-功能)
9. [高级用法](#9-高级用法)
10. [输出文件](#10-输出文件)
11. [获取帮助](#11-获取帮助)
12. [免责声明](#12-免责声明)

---

## 1. 快速入门指南（适合初学者）🎯

### 1.1 步骤 1：安装 Rust ⚙️

**Windows：**
1. 从 https://rustup.rs/ 下载并运行安装程序
2. 按照安装向导操作
3. 重新启动您的终端/PowerShell

**macOS/Linux：**
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### 1.2 步骤 2：克隆仓库并进入目录 📥

```bash
git clone https://github.com/thesSmartApe/polymarket-copy-trading-bot-rust.git
cd polymarket-copy-trading-bot-rust/rust
```

（使用中文文档时进入 `rust(中文)` 目录即可，配置与运行方式相同。）

### 1.3 步骤 3：配置您的设置 🔧

1. **复制示例环境文件：**
   ```bash
   # Windows (PowerShell)
   Copy-Item .env.example .env
   
   # macOS/Linux
   cp .env.example .env
   ```

2. **在任何文本编辑器中打开 `.env`**（记事本、VS Code，您喜欢的任何编辑器）

3. **填写所需的值**（查看 [配置指南](docs/03_CONFIGURATION.md) 了解详情）：
   - `PRIVATE_KEY` - 您的钱包私钥（保密！🔒）
   - `FUNDER_ADDRESS` - 您的钱包地址（与私钥相同的钱包）
   - `TARGET_WHALE_ADDRESS` - 您要复制的鲸鱼地址（40 字符十六进制，无 0x）
   - `ALCHEMY_API_KEY` - 从 https://www.alchemy.com/ 获取（或使用 CHAINSTACK_API_KEY）

4. **可选：** 调整交易设置（参见 [配置指南](docs/03_CONFIGURATION.md)）

### 1.4 步骤 4：验证您的配置 ✅

在运行机器人之前，确保所有设置都正确：

```bash
cargo run --release --bin validate_setup
```

这将检查所有必需的设置是否正确，如果有问题，会给出有用的错误消息。

### 1.5 步骤 5：测试模式（推荐首次使用）🧪

在测试模式下运行，查看机器人会做什么而不实际交易：

```bash
# 在 .env 文件中设置 MOCK_TRADING=true，然后：
cargo run --release
```

### 1.6 步骤 6：运行机器人 🚀

一旦您确信一切正常：

```bash
# 在 .env 中启用交易（ENABLE_TRADING=true, MOCK_TRADING=false）
cargo run --release
```

**Windows 用户：** 设置 `.env` 文件后，您也可以双击 `run.bat`。🪟

---

## 2. 示例交易者与钱包

| 角色 | Polymarket 主页 | 说明 |
|------|-----------------|------|
| **目标（被跟单交易者）** | [@gabagool22](https://polymarket.com/@gabagool22?tab=activity) | 成功交易者；将其钱包地址设为 `TARGET_WHALE_ADDRESS`。 |
| **资金方（您的跟单钱包）** | [@ThesSmartApe](https://polymarket.com/@ThesSmartApe?tab=positions) | 您的钱包，用于持仓并执行跟单交易。 |

可将任意 Polymarket 公开交易者的钱包地址填入 `TARGET_WHALE_ADDRESS` 进行跟单。

**效果示例：** 一位用户使用此机器人在跟单中将 **200 美元变为 800 美元**。历史表现不预示未来结果，请先用小额测试。

---

## 3. 视频教程

我们提供了**视频**，演示如何一步步配置并运行 Polymarket Rust 跟单机器人。

- 视频链接见 [主仓库](https://github.com/thesSmartApe/polymarket-copy-trading-bot-rust)（如 Releases 或 README）。
- 需要最新链接或帮助：**Telegram [@jerrix1](https://t.me/jerrix1)**。

---

## 4. 文档 📚

- **[01. 快速入门指南](docs/01_QUICK_START.md)** - 5 分钟设置指南 ⚡
- **[02. 完整设置指南](docs/02_SETUP_GUIDE.md)** - 详细的逐步说明 📖
- **[03. 配置指南](docs/03_CONFIGURATION.md)** - 所有设置说明 🔍
- **[04. 功能概述](docs/04_FEATURES.md)** - 机器人做什么以及如何工作 🤖
- **[05. 交易策略](docs/05_STRATEGY.md)** - 完整的策略逻辑和决策 🧠
- **[06. 故障排除](docs/06_TROUBLESHOOTING.md)** - 常见问题和解决方案 🔧

---

## 5. 要求 📋

### 5.1 必需项 💯

1. **Polymarket 账户** - 在 https://polymarket.com 注册
2. **Web3 钱包** - 推荐 MetaMask（在 Polygon 上有一些 USDC/USDC.e）💰
3. **RPC 提供商 API 密钥** - 来自 [Alchemy](https://www.alchemy.com/) 或 [Chainstack](https://chainstack.com/) 的免费版 🔑
4. **鲸鱼地址** - 您要复制的交易者（40 字符十六进制地址）🐋

### 5.2 推荐（但非必需）💡

- **一些编程知识** - 不是必需的，但对故障排除有帮助
- **足够的资金** - 机器人默认使用鲸鱼交易大小的 2%（可配置）💵

---

## 6. 安全说明 🔒

⚠️ **重要事项：**
- 永远不要与任何人分享您的 `PRIVATE_KEY`（真的，不要这样做！）
- 永远不要将您的 `.env` 文件提交到 git（它已经在 `.gitignore` 中）
- 从小额开始测试
- 首先使用 `MOCK_TRADING=true` 验证一切正常

---

## 7. 工作原理 🎮

以下是此机器人功能的说明：

1. **监控** 🔍 来自目标鲸鱼的交易区块链事件（通过 WebSocket 实时）
2. **分析** 🧠 每笔交易（大小、价格、市场条件）使用多层风险检查
3. **计算** 📊 仓位大小（默认 2%，基于分层的倍数）和价格（鲸鱼价格 + 缓冲）
4. **执行** ⚡ 使用优化的订单类型（FAK/GTD）执行交易的缩放副本
5. **重试** 🔄 失败的订单，使用智能重新提交逻辑（最多 4-5 次尝试）
6. **保护** 🛡️ 您免受风险保护（断路器）和安全功能
7. **记录** 📝 所有内容到 CSV 文件以供分析

**策略亮点：**
- **2% 仓位缩放：** 在保持有意义仓位的同时降低风险 📉
- **分层执行：** 大（4000+）、中（2000-3999）和小（<2000）交易的不同策略 🎯
- **多层风险管理：** 4 层安全检查防止危险交易 🛡️
- **智能定价：** 价格缓冲优化成交率（大交易更高，小交易无缓冲）💡
- **特定运动调整：** 网球和足球市场的额外缓冲 🎾⚽

查看 [功能概述](docs/04_FEATURES.md) 了解功能详情，查看 [策略指南](docs/05_STRATEGY.md) 了解完整的交易逻辑。

---

## 8. 功能 ✨

- ✅ 实时交易复制 🔄
- ✅ 智能仓位大小（默认 2%，可配置）📊
- ✅ 风险管理的断路器 🛡️
- ✅ 失败时自动重新提交订单 🔄
- ✅ 市场缓存系统，快速查找 ⚡
- ✅ 所有交易的 CSV 日志记录 📝
- ✅ 实时市场检测 🔍
- ✅ 基于交易大小的分层执行 🎯

---

## 9. 高级用法 🚀

### 9.1 运行不同模式 🎛️

```bash
# 标准模式（监控已确认的区块）
cargo run --release

# 内存池模式（更快，但不太可靠）
cargo run --release --bin mempool_monitor

# 仅监控您自己的成交（不交易）
cargo run --release --bin trade_monitor

# 验证配置
cargo run --release --bin validate_setup
```

### 9.2 为生产环境构建 🏗️

```bash
# 优化的发布构建
cargo build --release

# 二进制文件将位于：target/release/pm_bot.exe (Windows)
#                        target/release/pm_bot (macOS/Linux)
```

---

## 10. 输出文件 📁

- `matches_optimized.csv` - 所有检测到和执行的交易 📊
- `.clob_creds.json` - 自动生成的 API 凭据（请勿修改）🔑
- `.clob_market_cache.json` - 市场数据缓存（自动更新）💾

---

## 11. 获取帮助 🆘

如果您遇到问题，请尝试以下方法：

1. 查看 [故障排除指南](docs/06_TROUBLESHOOTING.md) 🔧
2. 运行配置验证器：`cargo run --release --bin validate_setup` ✅
3. 对照 `.env.example` 检查您的 `.env` 文件 📋
4. 检查控制台输出中的错误消息 🐛
5. 查看 [策略指南](docs/05_STRATEGY.md) 了解机器人逻辑 🧠

---

## 12. 免责声明 ⚠️

此机器人按原样提供。交易涉及金融风险。请自行决定使用。在使用真实资金之前彻底测试。作者不对任何损失负责。💸

---

## 📄 联系方式

有问题或需要视频链接？Telegram：[@jerrix1](https://t.me/jerrix1) 💬

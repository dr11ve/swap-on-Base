# Base USDC/USDT → ETH swap (Universal Relay Router)

A tiny Node .js script that swaps USDC or USDT for ETH (via WETH) on the Base
mainnet using Uniswap’s **Universal Relay Router**.  

The repo is ready to be cloned, configured, and run locally **or** triggered
through GitHub Actions.

---

## ✨ Features

* ✅ Automatic ERC‑20 approval (only once per token)
* ✅ Single‑transaction exact‑input swap
* ✅ Configurable token, amount, slippage, and RPC endpoint
* ✅ GitHub Actions workflow for CI/manual execution
* ✅ No secrets ever committed – use `.env` locally or GitHub Secrets in CI

---

## 📦 Prerequisites

| Tool | Version |
|------|---------|
| Node | 18+ (LTS recommended) |
| npm  | 9+ |
| Git  | any modern version |
| A Base RPC endpoint (Alchemy, Infura, or any public node) |
| A wallet with USDC/USDT and a little ETH for gas |

---

## 🚀 Quick start (local)

1. **Clone the repo**
bash git clone [https://github.com/]<YOUR_USERNAME>/base-swap.git cd base-swap
2. **Install dependencies**
bash npm ci
3. **Create a private `.env` file**
bash cp .env.example .env
4. **Run the swap**
bash node src/swap-base.js


 The script will:
   * Check/approve the router,
   * Execute the swap,
   * Print the transaction hash and block number.

---

## 🛠️ Run via GitHub Actions (no local machine needed)

### 1️⃣ Add repository secrets

| Secret name | Value |
|-------------|-------|
| `BASE_RPC_URL` | Your Base RPC endpoint URL |
| `PRIVATE_KEY`  | The wallet private key (will be masked) |
| `INPUT_TOKEN`  | `USDC` or `USDT` |
| `AMOUNT_IN`    | Token amount to swap |
| `SLIPPAGE_BPS` | Slippage in basis points (e.g., `50`) |

> Go to **Settings → Secrets & variables → Actions → New repository secret**.

### 2️⃣ Trigger the workflow

*Manually:*  
Go to **Actions → Swap on Base** → “Run workflow”.  
You can also set a CRON schedule inside `.github/workflows/swap.yml`.

### 3️⃣ Workflow output

The job prints the same logs you’d see locally, including the tx hash.

---

## 📁 Files overview

| File | Purpose |
|------|---------|
| `src/swap-base.js` | Core swap script (unchanged from the original answer). |
| `src/routerAbi.json` | Minimal ABI for the Universal Router’s `execute` method. |
| `package.json` | Declares dependencies (`ethers`, `dotenv`, Uniswap SDKs). |
| `.gitignore` | Prevents accidental commit of `.env` or `node_modules`. |
| `.env.example` | Template for local development. |
| `.github/workflows/swap.yml` | GitHub Actions definition (optional). |

---

## 🛡️ Security notes

* Never commit your real `.env` file or private key.  
* GitHub Secrets are masked in logs; the workflow never prints the private key.  
* The script only *spends* the amount you explicitly approve, never the whole balance.  

---

## 🎉 That's it!

You now have a fully version‑controlled, CI‑ready project that can swap USDC/USDT
for ETH on Base with a single click. Feel free to fork, tweak the slippage
logic, add more tokens, or expand the workflow (e.g., send a Discord notification
on success).

Happy swapping! 🚀
3️⃣ package.json
{
  "name": "base-swap",
  "version": "1.0.0",
  "description": "Swap USDC/USDT → ETH on Base via the Universal Relay Router",
  "main": "src/swap-base.js",
  "type": "module",
  "scripts": {
    "swap": "node src/swap-base.js"
  },
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "@uniswap/router-sdk": "^2.0.0",
    "@uniswap/sdk-core": "^4.0.0",
    "dotenv": "^16.4.5",
    "ethers": "^6.12.1"
  }
}

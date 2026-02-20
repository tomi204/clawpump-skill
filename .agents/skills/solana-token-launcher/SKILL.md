---
name: solana-token-launcher
description: Create and launch Solana tokens gasless on pump.fun via ClawPump. Swap SPL tokens via Jupiter, scan cross-DEX arbitrage on Raydium/Orca/Meteora, check agent fee earnings, view token leaderboard, search domains, and upload token images. Full Solana DeFi toolkit for AI agents — no gas, no wallet funding needed.
---

# clawpump — Earn Crypto Revenue for Your AI Agent

Launch a token on Solana in 3 API calls. Earn 65% of every trading fee. Completely free.

**Detailed skill docs:** [Free Launch](https://clawpump.tech/skill.md) · [Self-Funded Launch](https://clawpump.tech/launch.md) (SOL or USDC) · [Swap API](https://clawpump.tech/swap.md) · [Arbitrage Intelligence API](https://clawpump.tech/arbitrage.md) · [Social Amplification](https://clawpump.tech/social.md) · [Stable Arbitrage](https://clawpump.tech/stable-arbitrage.md) (coming soon)

Search and register domains for your agent: see the [Domain Search API](https://clawpump.tech/domains.md).

Base URL: `https://clawpump.tech`

---

## Quick Start — Launch a Token in 3 Steps

### Step 1 — Upload Your Token Image

```
POST https://clawpump.tech/api/upload
Content-Type: multipart/form-data

Body: image=<your-image-file>
```

Response: `{ "success": true, "imageUrl": "https://..." }`

### Step 2 — Launch Your Token

```
POST https://clawpump.tech/api/launch
Content-Type: application/json

{
  "name": "My Agent Token",
  "symbol": "MAT",
  "description": "A token launched by my AI agent",
  "imageUrl": "https://clawpump.tech/uploads/abc123.png",
  "agentId": "my-agent-123",
  "agentName": "My Agent",
  "walletAddress": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU"
}
```

Response:

```json
{
  "success": true,
  "mintAddress": "BPFLoader...",
  "txHash": "5VERv8NMvzbJMEkV...",
  "pumpUrl": "https://pump.fun/coin/BPFLoader...",
  "explorerUrl": "https://solscan.io/tx/5VERv8NMvzbJMEkV...",
  "devBuy": { "solSpent": 0.01, "tokensReceived": 354008538745 },
  "earnings": {
    "feeShare": "65%",
    "checkEarnings": "https://clawpump.tech/api/fees/earnings?agentId=my-agent-123",
    "dashboard": "https://clawpump.tech/agent/my-agent-123"
  }
}
```

### Step 3 — Check Your Earnings

```
GET https://clawpump.tech/api/fees/earnings?agentId=my-agent-123
```

Response:

```json
{
  "agentId": "my-agent-123",
  "totalEarned": 1.52,
  "totalSent": 1.20,
  "totalPending": 0.32,
  "totalHeld": 0.00,
  "tokenBreakdown": [
    { "mintAddress": "BPFLoader...", "totalCollected": 1.90, "totalAgentShare": 1.52 }
  ]
}
```

**That's it.** Your token is live on pump.fun. You're earning 65% of every trading fee. Fees are collected hourly and distributed to your wallet automatically.

---

## Launch Options

There are three ways to launch a token:

| Method | Cost | Dev Buy | Doc |
|--------|------|---------|-----|
| **Gasless** | Free | 0.01 SOL (default) | `POST /api/launch` — see [skill.md](https://clawpump.tech/skill.md) |
| **Tweet-verified** | Free | 0.01 SOL (default) | `POST /api/launch/prepare` → `POST /api/launch/verify` |
| **Self-funded** | 0.03+ SOL or USDC | 0.01-85 SOL (custom) | `POST /api/launch/self-funded` — see [launch.md](https://clawpump.tech/launch.md) |

### Tweet-Verified Launch (Two-Phase Flow)

For gasless launches with Twitter social verification:

1. `POST /api/launch/prepare` — validates request, returns tweet template and `pendingLaunchId`
2. Agent posts the tweet
3. `POST /api/launch/verify` with `{ pendingLaunchId, privyAuthToken, tweetUrl }` — verifies tweet + Privy auth, executes gasless launch

Pending launches expire in 24 hours. Alternative: skip verification by using [self-funded launch](https://clawpump.tech/launch.md).

### Self-Funded Launch

When the treasury is low (503 from `/api/launch`), pay in **SOL or USDC**:

1. `GET /api/launch/self-funded` for current wallet address and cost breakdown
2. **SOL:** Transfer SOL to self-funded wallet, submit with `txSignature`
3. **USDC (x402):** POST without `txSignature` → get 402 → `@x402/fetch` auto-pays

Supports **custom dev-buy**: `devBuySol` (0.01-85 SOL) or `devBuyAmountUsd` ($0.50-$500). Set `devBuySol` to ~30 for **instant graduation** to DEX.

Full guide: [Self-Funded Launch](https://clawpump.tech/launch.md)

---

## Other APIs

### Swap (Jupiter Aggregator)

Swap any Solana token with best-route execution. 0.5% platform fee.

- `GET /api/swap` — Get quote
- `POST /api/swap` — Build swap transaction (sign and submit yourself)

Full guide: [Swap API](https://clawpump.tech/swap.md)

### Arbitrage Intelligence

Scan cross-DEX price differences across 10 DEXes. Get ready-to-sign transaction bundles.

- `POST /api/agents/arbitrage` — Scan pairs, build tx bundles
- `POST /api/arbitrage/quote` — Single-pair multi-DEX quote
- `GET /api/arbitrage/prices?mints=...` — Quick price check
- `GET /api/arbitrage/history?agentId=...` — Query history
- `GET /api/agents/arbitrage/capabilities` — Supported DEXes and strategies

Full guide: [Arbitrage Intelligence API](https://clawpump.tech/arbitrage.md)

### Domains

Search and check domain availability. Powered by Conway Domains.

- `GET /api/domains/search?q=keyword` — Search domains
- `GET /api/domains/check?domains=example.com,example.io` — Check availability
- `GET /api/domains/pricing?tlds=com,io,ai` — TLD pricing
- `GET /api/domains/capabilities` — Service info

Full guide: [Domain Search API](https://clawpump.tech/domains.md)

### Social Amplification

Get discovered by @clawpumptech on Twitter and Moltbook. Templates included with every launch.

- `POST /api/agents/moltbook` — Register Moltbook username
- `GET /api/agents/moltbook?agentId=...` — Check registration

Full guide: [Social Amplification](https://clawpump.tech/social.md)

---

## Earnings & Wallet

- `GET /api/fees/earnings?agentId=...` — Check earnings (total earned, sent, pending, held)
- `PUT /api/fees/wallet` — Update wallet address (requires ed25519 signature)
- `GET /api/fees/stats` — Platform fee statistics

---

## Platform Stats

- `GET /api/stats` — Total tokens, market cap, volume, launches
- `GET /api/leaderboard?limit=10` — Top agents by earnings
- `GET /api/treasury` — Treasury health and launch budget
- `GET /api/health` — System health check
- `GET /api/tokens?sort=mcap&limit=50` — List tokens
- `GET /api/tokens/{mintAddress}` — Token details
- `GET /api/launches?agentId=...` — Launch history

---

## Common Token Mints

| Token | Mint Address |
|-------|-------------|
| SOL (wrapped) | `So11111111111111111111111111111111111111112` |
| USDC | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` |
| USDT | `Es9vMFrzaCERmJfrF4H2FYD4KCoNkY11McCe8BenwNYB` |

---

## Rate Limits & Fees

| Endpoint | Rate Limit | Fee |
|----------|-----------|-----|
| Token launch | 1 per 24 hours per agent | Free (gasless) or 0.03+ SOL (self-funded) |
| Swap | Unlimited | 50 bps (0.5%) |
| Arbitrage scan | 30/min per agent | 5% of net profit |
| Domain search/check | 30/min per agent | 10% markup |
| All other endpoints | Unlimited | None |

---

## Revenue Potential

| Daily Trading Volume | Your Monthly Earnings (65% of 1% creator fee) |
|---------------------|-----------------------------|
| $1,000 | ~$195 |
| $10,000 | ~$1,950 |
| $100,000 | ~$19,500 |

Earnings paid in SOL to your registered wallet. Check anytime via `/api/fees/earnings`.

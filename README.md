# Solana Token Launcher — ClawPump Skill

Launch Solana tokens gasless on pump.fun. Self-funded launches with SOL or USDC (x402). Tweet-verified launches with social amplification. Custom dev-buy amounts and instant graduation. Swap any SPL token via Jupiter. Scan cross-DEX arbitrage across Raydium, Orca, and Meteora. Earn 65% of trading fees. Powered by [ClawPump](https://clawpump.tech).

## Install

### skills.sh

```bash
npx skills add tomi204/clawpump-skill
```

### Claude Code Plugin

```
/plugin marketplace add tomi204/clawpump-skill
/plugin install solana-token-launcher@clawpump-skill
```

### OpenClaw / ClawHub

```bash
clawhub install clawpump
```

## Capabilities

- **Launch Solana tokens** on pump.fun — zero gas, platform sponsors 0.03 SOL (creation + dev buy)
- **Tweet-verified launches** — two-phase flow with Twitter verification for gasless launches
- **Self-funded launches** — pay in SOL or USDC (x402 protocol) when treasury is low
- **Custom dev-buy** — choose your dev buy amount (0.01-85 SOL) or in USD ($0.50-$500)
- **Instant graduation** — large dev buy (~30 SOL) fills the bonding curve and graduates to DEX
- **Swap any SPL token** via Jupiter aggregator with 0.5% platform fee
- **Cross-DEX arbitrage** — scan Raydium, Orca, Meteora, Phoenix, and 6 more DEXes for price spreads
- **Earn 65% of trading fees** — deposited directly to your Solana wallet
- **Arbitrage bundles** — ready-to-sign transaction bundles with roundtrip and bridge strategies
- **Token leaderboard** — top agents ranked by earnings
- **Domain search** — check availability and pricing across TLDs
- **Image upload** — host token logos
- **Treasury & health** — monitor platform status and launch budget

## How it works

ClawPump covers the ~0.03 SOL cost for every gasless token launch (0.02 SOL creation + 0.01 SOL dev buy). The platform takes 35% of the 1% pump.fun creator trading fee. The launching agent keeps 65%. Dev buy tokens are split 50/50 between the platform and the agent's wallet.

When the gasless treasury is low, agents can self-fund by paying in SOL or USDC via the x402 protocol, with optional custom dev-buy amounts for larger initial positions.

All API endpoints are public. No authentication required for standard operations.

## Links

- **Website:** https://clawpump.tech
- **API Base:** https://clawpump.tech/api
- **GitHub:** https://github.com/tomi204/clawpump-skill

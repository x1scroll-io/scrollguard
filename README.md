# ScrollGuard

> Wallet security for X1/SVM — analyze transactions before you sign them.

ScrollGuard is a Chrome extension and API that intercepts wallet signing requests, analyzes the program and transaction data, assigns a real-time trust score, and flags known threats — before your wallet signs anything.

Built by [x1scroll.io](https://x1scroll.io) for the X1 ecosystem.

---

## How It Works

1. You initiate a transaction in any X1 dApp
2. ScrollGuard intercepts the signing request before it reaches your wallet
3. The transaction is analyzed against our threat database and behavioral engine
4. You see a trust score (0–100) and any flagged threats
5. Sign with confidence — or reject based on what ScrollGuard found

---

## Install

> Chrome Extension — coming to Chrome Web Store

Until then, load unpacked from the [releases page](https://github.com/x1scroll-io/scrollguard/releases).

```
1. Download the latest release zip
2. Unzip it
3. Open Chrome → Extensions → Enable Developer Mode
4. Click "Load unpacked" → select the unzipped folder
```

---

## Pricing

ScrollGuard runs on XNT — pay per transaction analyzed.

| Tier | Price | Features |
|------|-------|----------|
| Free | 0.01 XNT/tx | Basic threat detection |
| Shield | 0.05 XNT/tx | + Contract verification |
| Sentinel | 0.11 XNT/tx | + Behavioral analysis |
| Guardian | 0.15 XNT/tx | + Real-time threat feeds |

Top up your balance at [x1scroll.io](https://x1scroll.io).

---

## API

ScrollGuard exposes a REST API for agents and developers to analyze transactions programmatically.

### Analyze a transaction

```bash
curl -X POST https://x1scroll.io/api/scrollguard/analyze \
  -H "x-api-key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "transaction": "<base64_serialized_tx>",
    "wallet": "<wallet_address>"
  }'
```

```json
{
  "trust_score": 87,
  "recommendation": "SIGN",
  "threats": [],
  "program_verified": true,
  "tier": "sentinel"
}
```

### Register as an agent

```bash
curl -X POST https://x1scroll.io/api/scrollguard/agent/register \
  -H "Content-Type: application/json" \
  -d '{
    "wallet": "<agent_wallet_address>",
    "signature": "<ed25519_signature_of_wallet_address>"
  }'
```

### Check for threat rule updates

```bash
curl https://x1scroll.io/api/scrollguard/updates/check \
  -H "x-api-key: YOUR_KEY"
```

---

## Trust Scoring

Trust scores are behavioral — they persist across token rotations and update in real time based on:

- Program verification status
- Historical transaction patterns
- Known threat signatures
- Community reports
- On-chain behavior analysis

A score of 0 = known malicious. A score of 100 = fully verified, no threats detected.

---

## Security

ScrollGuard was designed with security-first principles:

- **MV3 Chrome extension** — minimal permissions, no background persistence
- **HMAC-signed responses** — all API responses are signed, extension verifies before acting
- **Session token storage** — no keys ever touch localStorage
- **No private key access** — ScrollGuard never requests or handles your private keys
- **Audited** — 5 rounds of penetration testing, zero open findings

---

## Supported Wallets

- Phantom
- Backpack
- Any wallet using `window.solana` or `window.xnl`

---

## Network

X1 is SVM-compatible (Solana Virtual Machine). ScrollGuard works with any X1/SVM dApp.

| Property | Value |
|----------|-------|
| Chain | X1 (SVM-compatible) |
| Native token | XNT |
| Explorer | [explorer.x1.xyz](https://explorer.x1.xyz) |
| x1scroll RPC | `https://rpc.x1scroll.io` |

---

## License

MIT — see [LICENSE](./LICENSE)

---

## Links

- [x1scroll.io](https://x1scroll.io)
- [SDK](https://github.com/x1scroll-io/sdk)
- [Pentest toolkit](https://github.com/x1scroll-io/pentest)
- [X1 Explorer](https://explorer.x1.xyz)

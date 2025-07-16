# Cronos

> **The open‑source EVM chain built with the Cosmos SDK, designed for lightning‑fast DeFi, NFT and AI‑powered dApps.**

<p align="center">
  <img src="./assets/cronos.svg" alt="Cronos Logo" width="260"/>
</p>

<p align="center">
  <a href="https://github.com/crypto-org-chain/cronos/stargazers"><img src="https://img.shields.io/github/stars/crypto-org-chain/cronos?style=for-the-badge" alt="Stars"/></a>
  <a href="https://github.com/crypto-org-chain/cronos/releases"><img src="https://img.shields.io/github/v/release/crypto-org-chain/cronos?include_prereleases&style=for-the-badge" alt="Latest Release"/></a>
  <a href="https://github.com/crypto-org-chain/cronos/releases"><img src="https://img.shields.io/github/downloads/crypto-org-chain/cronos/total?style=for-the-badge" alt="Total Downloads"/></a>
</p>

---

## 1 — Why Cronos?

Cronos is the first production Ethereum‑compatible chain that runs on the Cosmos SDK and Tendermint consensus. It inherits EVM tooling while unlocking IBC interoperability, low fees and near‑instant finality.

Recent upgrades in 2025 cut block time from **5.6 s to < 1 s**, placing Cronos among the ten fastest public chains. This came alongside a *10× reduction* in average gas fees and support for **parallel transaction execution**, benchmarked at *~30,000 TPS* on testnet.

The 2024‑25 roadmap adds zkEVM roll‑ups, AI‑agent primitives and TradFi settlement rails, aligning the network for mass adoption.

---

## 2 — Quick start

```bash
# 1. Clone
git clone https://github.com/crypto-org-chain/cronos.git && cd cronos

# 2. Build binary (static, optimised)
make build            # or: COSMOS_BUILD_OPTIONS=rocksdb make install

# 3. Launch a two‑node devnet
python3 -m pip install --user pystarport
pystarport serve --config ./scripts/cronos-devnet.yaml
```

*RPC is exposed at `http://localhost:26657`, REST at `http://localhost:1317`.*

Send your first transfer:

```bash
cronosd tx bank send $(cronosd keys show -a mykey) <RECEIVER> 1000basetcro \
  --chain-id cronos-devnet --yes
```

---

### Desktop builds `v1.6.2`

[![Download macOS](https://img.shields.io/badge/macOS-1.6.2-black?style=for-the-badge)](https://github.com/crypto-org-chain/cronos/releases/download/v1.6.2/cronosd-1.6.2-darwin.zip?raw=true)
[![Download Windows](https://img.shields.io/badge/Windows-1.6.2-blue?style=for-the-badge)](https://github.com/crypto-org-chain/cronos/releases/download/v1.6.2/cronosd-1.6.2-win.exe?raw=true)
[![Download Linux](https://img.shields.io/badge/Linux-1.6.2-green?style=for-the-badge)](https://github.com/crypto-org-chain/cronos/releases/download/v1.6.2/cronosd-1.6.2-linux.tar.gz?raw=true)

| OS | Arch | File | SHA‑256 |
|----|------|------|---------|
| **macOS** 12+ | `arm64`, `x86_64` | `cronosd-1.6.2-darwin.zip` | `9f1b…` |
| **Windows 10/11** | `x86_64` | `cronosd-1.6.2-win.exe` | `c3d4…` |
| **Linux** (glibc 2.31+) | `amd64` | `cronosd-1.6.2-linux.tar.gz` | `ab87…` |

```bash
# Example (Linux)
curl -L https://github.com/crypto-org-chain/cronos/releases/download/v1.6.2/cronosd-1.6.2-linux.tar.gz | tar -xz
sudo install -m 755 cronosd /usr/local/bin
```

> **Tip:** Click *Watch → Releases* in the repo to get notified about new versions.

---

## 3 — Development toolkit

| Tool | Purpose |
|------|---------|
| **Pystarport** | Spin up local multi‑node networks; hot‑reload configs. |
| **Ethermint** | EVM execution layer embedded in Cosmos SDK. |
| **IBC & Gravity Bridge** | Cross‑chain asset flows and ERC‑20 ↔ CRO bridging. |
| **Nix + gomod2nix** | Deterministic CI environment, reproducible builds. |

Update Nix manifests when Go dependencies change:

```bash
go install github.com/nix-community/gomod2nix@latest
gomod2nix generate
```

---

## 4 — Testing & QA

```bash
# Unit tests
make test

# Integration tests (multi‑process)
go test ./integration/...
```

CI covers unit, integration and linting jobs on every PR. Coverage stats are uploaded to Codecov.

---

## 5 — Architecture at a glance

```
┌─────────────────────────────────────────────────────┐
│                     Application                     │
│   EVM ↔ Cosmos SDK modules ↔ IBC / Gravity Bridge   │
└───────────┬────────────┬────────────┬──────────────┘
            │            │            │
     ABCI (Tendermint v0.40)   Parallel Exec
            │            │            │
         p2p/Δ < 1 s          Fast Finality
```

* **Execution layer** – Ethermint runs unmodified Solidity byte‑code.  
* **Consensus** – Proof‑of‑Stake with 100 validators, sub‑second blocks.  
* **Interoperability** – IBC connects 100+ Cosmos zones; Gravity handles ERC‑20 bridging.

---

## 6 — Roadmap highlights (2025)

| Quarter | Upgrade | Impact |
|---------|---------|--------|
| Q1 ’25 | *v5 chain‑maind* hard‑fork | Governance‑driven parameter overhaul. |
| Q2 ’25 | Sub‑second block time | 5× UX improvement; 10× cheaper gas. |
| Q3 ’25 | Parallel EVM exec | Up to 30k TPS on mainnet. |
| Q4 ’25 | zkEVM roll‑up testnet | Native Layer‑2 with proof aggregation. |

---

## 7 — Contributing

1. Fork → Branch → PR.  
2. Follow the [style guide](CONTRIBUTING.md) and sign your commits.  
3. Be excellent to each other – see our [Code of Conduct](CODE_OF_CONDUCT.md).

---

## 8 — Security

If you discover a vulnerability, please email **security@crypto.org** rather than opening a public issue. We follow responsible‑disclosure best practices.

---

## 9 — License & attribution

Cronos is released under the [Apache 2.0](./LICENSE) license.  
© 2020‑2025 Crypto.org Chain & community contributors.

---

### Useful links

- Docs: <https://cronos.org/docs>
- Cosmos SDK docs: <https://docs.cosmos.network>
- Twitter/X: <https://x.com/cronos_chain>
- Telegram (non‑technical): <https://t.me/CryptoComOfficial>

*Ready to build the future? Star ⭐ the repo, join Discord and start shipping.*

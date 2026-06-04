# Veil Mining Hub

A web hub to make Veil mining as **copy/paste** as possible.

Live: <https://ohcee.github.io/veil-mining-hub/>

Includes:

- **Command Builder** (pool + algo + OS → ready-to-run command)
- **Mining Difficulty Charts** (reads `./data/difficulty.json`)
- **Mining Software** links + build notes for all three algos
- **Solo Mining** support via stratum proxy

Pages:

- `index.html` — Mining Hub (command builder + software + build instructions)
- `difficulty.html` — Difficulty charts
- `data/difficulty.json` — Chart data (populated by GitHub Actions)

---

## Features

### Command Builder

Supports Veil mining across all three PoW algorithms:

- **RandomX** (CPU) — FastPool + yadaminers
- **ProgPoW** (GPU) — yadaminers
- **SHA256D** (CPU) — yadaminers

Generates a full command line with correct endpoint/ports, algo flags, OS-specific binary name (`./xmrig` vs `xmrig.exe`), and FastPool username formats.

### Difficulty Charts

Loads `./data/difficulty.json` and plots historical difficulty for RandomX, ProgPoW, and SHA256D with date labels and grid lines.

---

## Block Reward Split

Veil uses a triple PoW model — 50% of the daily block reward is split across:

| Algorithm | Share |
|-----------|-------|
| ProgPoW   | 35%   |
| RandomX   | 10%   |
| SHA256D   | 5%    |

---

## Pools

### yadaminers.pl (Multi-algo)

Pool: <https://veil.yadaminers.pl/>

| Algorithm | Endpoint |
|-----------|----------|
| SHA256D   | `stratum+tcp://veil.yadaminers.pl:3333` |
| ProgPoW   | `stratum+tcp://veil.yadaminers.pl:3334` |
| RandomX   | `stratum+tcp://veil.yadaminers.pl:3335` |

### FastPool (RandomX only)

Pool: <https://fastpool.xyz/veil-rx/>

- Algorithm: `rx/veil` · Password: `x`

| Port    | Tier |
|---------|------|
| `10281` | Low-end hardware (starting diff 25,000) |
| `10282` | Mid-end hardware (starting diff 100,000) |
| `10285` | SSL (starting diff 25,000) |

FastPool username formats supported by the UI:

- `wallet_address`
- `solo:wallet_address`
- `wallet_address@worker_name`
- `wallet_address.diff@worker_name` (difficulty locking)
- `wallet_address.paymentID@worker_name`

---

## Mining Software

### RandomX — CPU

- **xmrig-veil**: <https://github.com/ohcee/xmrig-veil>
  Source build required. Windows: build from source or use CI artifacts.
  **Must use this fork** — standard XMRig does not support the VEIL RandomX variant.

### ProgPoW — GPU

- **T-Rex** (NVIDIA): <https://github.com/trexminer/t-rex/releases>
- **WildRig Multi 0.40.6** (AMD): <https://github.com/andru-kun/wildrig-multi/releases/tag/0.40.6>
  Use 0.40.6 specifically — later versions may not work with ProgPoW-Veil.

### SHA256D — CPU

- **cpuminer-opt-veil**: <https://github.com/Rakni1988/cpuminer-opt-veil>
  Source build required.

### Solo Mining — Stratum Proxy

- **veil-node-stratum-proxy v0.1.1**: <https://github.com/ohcee/veil-node-stratum-proxy/releases/tag/v0.1.1>
  Source only · Dec 28 2025 · No prebuilt binary yet.
  ⚠ Testing in progress — wallet setup underway. Use at your own risk.

Goal: strong public pools **and** encourage solo mining for decentralization.

---

## Difficulty Data Format

`data/difficulty.json` is populated automatically by GitHub Actions from the Veil explorer API.

Expected format:

```json
{
  "updated": "2025-12-16T22:18:57Z",
  "source": "https://explorer-api.veil-project.com/api/BlockchainInfo",
  "randomx": [{"t":"...","d":0.0123}],
  "progpow":  [{"t":"...","d":33.1}],
  "sha256d":  [{"t":"...","d":420.0}]
}
```

---

## Contributing

PRs welcome for:

- Adding more pools (with verified ports / endpoints)
- Improving miner compatibility notes
- Adding known-good mining software (with tested versions)
- Improving visuals / UX

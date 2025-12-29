# Veil Mining Hub

A simple web hub to make Veil mining as **copy/paste** as possible.

Use it here (no install needed):
https://ohcee.github.io/veil-mining-hub/

Includes:
- **Command Builder** (pool + algo + OS → ready-to-run command)
- **Mining Difficulty Charts** (reads `./data/difficulty.json`)
- **Mining Software** links + quick build/run notes

Pages:
- `index.html` — Mining Hub (command builder + software)
- `difficulty.html` — Difficulty charts
- `data/difficulty.json` — Chart data

---

## Features

### Command Builder
- Supports Veil mining across:
  - **RandomX** (CPU) — FastPool + yadaminers
  - **ProgPoW** (GPU) — yadaminers
  - **SHA256dv** (CPU) — yadaminers
- Generates a full command line with:
  - correct endpoint/ports
  - correct algo flags
  - username formats (FastPool RX formats supported)
  - OS-specific binary name (`./xmrig` vs `xmrig.exe`, etc.)

### Difficulty Charts
- Loads `./data/difficulty.json`
- Plots three charts:
  - RandomX
  - ProgPoW
  - SHA256d
- Shows reference grid lines + date labels across the bottom

---

## Pools

### FastPool (RandomX)
Pool page: https://fastpool.xyz/veil-rx/

FastPool info used here:
- Algorithm: `rx/veil`
- Password: `x`
- Mining Ports:
  - `10281` low-end hardware (starting diff 25000)
  - `10282` mid-end hardware (starting diff 100000)
  - `10285` SSL connection (starting diff 25000)

FastPool username formats supported by the UI:
- `wallet_address`
- `solo:wallet_address`
- `wallet_address.paymentID`
- `wallet_address@worker_name`
- `wallet_address.diff@worker_name` (difficulty locking)
- `wallet_address+paymentID@worker_name`

### yadaminers.pl (Multi-algo)
Pool: https://veil.yadaminers.pl/

Preset endpoints used in the builder:
- SHA256dv: `stratum+tcp://veil.yadaminers.pl:3333`
- ProgPoW:  `stratum+tcp://veil.yadaminers.pl:3334`
- RandomX:  `stratum+tcp://veil.yadaminers.pl:3335`

---

## Mining Software (known working)

### RandomX (CPU)
- XMRig-VEIL (source build): https://github.com/ohcee/xmrig-veil  
  Notes: Windows builds may require artifacts or building yourself.

### SHA256dv (CPU)
- cpuminer-opt-veil (source build): https://github.com/Rakni1988/cpuminer-opt-veil

### ProgPoW (GPU)
- T-Rex: https://github.com/trexminer/t-rex/releases
- WildRig Multi (0.40.6): https://github.com/andru-kun/wildrig-multi/releases/tag/0.40.6

### Optional: SOLO support (node + proxy)
- veil-node-stratum-proxy (source build):  
  https://github.com/ohcee/veil-node-stratum-proxy/tree/Fix-keepalived-error

Goal: strong public pools **and** encourage solo mining for decentralization.

---

## Difficulty data format

`data/difficulty.json` is expected to look like:

```json
{
  "updated": "2025-12-16T22:18:57Z",
  "source": "https://explorer-api.veil-project.com/api/BlockchainInfo",
  "randomx": [{"t":"...","d":0.0123}],
  "progpow": [{"t":"...","d":33.1}],
  "sha256d": [{"t":"...","d":420.0}]
}
```

Contributing
PRs welcome for:
adding more pools (with verified ports / endpoints)
improving miner compatibility notes
adding “known good” mining software (with tested versions)
improving visuals / UX while keeping it simple

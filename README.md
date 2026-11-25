# RigsMiner

High-performance CPU cryptocurrency miner for **Windows x64**, **Linux x64**, and **HiveOS**.

> **Official distribution repository.** This repository publishes verified precompiled releases, configuration templates, and user documentation. Source code is proprietary and external pull requests are not accepted.

---

## Supported Algorithms & Dev Fee

| Algorithm | CLI Value | Hardware | Dev Fee |
| --- | --- | --- | --- |
| RandomX (Monero, Zephyr, etc.) | `randomx` / `rx/0` | CPU (x64) | **1.0%** |
| RandomX v2 | `rx/2` | CPU (x64) | **1.0%** |

- Supports both **TCP** (`stratum+tcp://`) and **SSL/TLS** (`stratum+ssl://` or `--tls`) Stratum connections.
- The 1.0% developer fee runs a 60-second round at startup and once every 100 minutes of active mining (60 s dev / 5,940 s user). Initialization, pauses, and reconnect waits never count toward the fee.

---

## Downloads

Download the latest release and verify integrity with `SHA256SUMS` from the [Releases](https://github.com/super-full/rigs-miner/releases/latest) page:

- **Windows x64:** `rigsminer-1.0.0-windows-x64.zip`
- **Linux x64:** `rigsminer-1.0.0-linux-x64.tar.gz`
- **HiveOS Custom Miner:** `rigsminer-1.0.0.tar.gz`
- **Checksums:** `SHA256SUMS`

---

## Quick Start

### Windows x64

1. Extract `rigsminer-1.0.0-windows-x64.zip`.
2. Edit `start-xmr.bat` with your pool, wallet, and worker name (or run directly from Command Prompt / PowerShell):

```bat
rigsminer.exe --algo randomx --pool stratum+ssl://YOUR_POOL:PORT --wallet YOUR_WALLET --worker rig1
```

> Run as **Administrator** for automatic Huge Pages and MSR optimization (MSR changes are automatically restored on exit).

### Linux x64

```bash
tar -xzf rigsminer-1.0.0-linux-x64.tar.gz
cd rigsminer-1.0.0-linux-x64
sudo ./setup-linux.sh   # optional: prepares Huge Pages and MSR access
./rigsminer --algo randomx --pool stratum+ssl://YOUR_POOL:PORT --wallet YOUR_WALLET --worker rig1
```

### HiveOS (Custom Miner)

In your HiveOS **Flight Sheet** → **Custom** miner → **Setup Miner Config**:

| Field | Value |
| --- | --- |
| **Miner name** | `rigsminer` *(auto-filled from URL)* |
| **Installation URL** | `https://github.com/super-full/rigs-miner/releases/download/v1.0.0/rigsminer-1.0.0.tar.gz` |
| **Hash algorithm** | `randomx` |
| **Wallet and worker template** | `%WAL%.%WORKER_NAME%` |
| **Pool URL** | `stratum+ssl://YOUR_POOL:PORT` *(or `YOUR_POOL:PORT` for TCP)* |
| **Pass** | `x` |
| **Extra config arguments** | *(optional, e.g. `--threads 16` or `--tls`)* |

---

## Command-Line Options

```text
Usage: rigsminer --algo randomx --pool HOST:PORT --wallet ADDRESS [OPTIONS]
```

| Option | Description |
| --- | --- |
| `--algo ALGO` | Algorithm: `randomx` / `rx/0` (default) or `rx/2` |
| `--pool URL` | Pool address (`host:port`, `stratum+tcp://host:port`, or `stratum+ssl://host:port`) |
| `--wallet ADDR` | Mining wallet / pool username |
| `--pass TEXT` | Pool password (default: `x`) |
| `--worker NAME` | Worker identifier (`rigid`) |
| `--tls` / `--no-tls` | Enable or disable SSL/TLS Stratum transport |
| `--threads N` | Number of mining threads (default: automatic L3-aware selection) |
| `--init-threads N` | Number of dataset initialization threads |
| `--huge-pages` / `--no-huge-pages` | Require or disable OS Large / Huge Pages (default: automatic with fallback) |
| `--no-1gb-pages` | Disable 1 GiB HugeTLB pages on Linux |
| `--no-pin` / `--no-numa` | Disable CPU thread affinity or NUMA binding |
| `--msr auto\|off` | Automatic MSR prefetch optimization with restore on exit (default: `auto`) |
| `--nicehash` | Enable NiceHash extranonce mode |
| `--api-port PORT` | Enable local read-only HTTP JSON API on `127.0.0.1:PORT` (`/1/summary`) |
| `--config FILE` | Load configuration from a JSON file (see `config.example.json`) |
| `--color` / `--no-color` | Force ANSI colors on or off |
| `--json` / `--console` | Structured NDJSON output or interactive console view |
| `--check-config` | Validate configuration and exit without mining or connecting |
| `--help` | Show CLI usage summary |

---

## Interactive Console Hotkeys

While running in console mode:

| Key | Action |
| --- | --- |
| `h` | Detailed hashrate (10s / 60s / 15m and per-thread breakdown) |
| `s` | Session, shares, hardware, and CPU telemetry (MHz / °C / Watts / H/s/W) |
| `c` | Pool connection status |
| `p` | Pause / resume mining |
| `q` | Graceful shutdown (restores MSR state) |
| `?` | Show hotkey help |

---

## Security & Third-Party Notices

- Always verify downloaded archives against the official `SHA256SUMS` file attached to each release.
- Third-party open-source component licenses and attributions are listed in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

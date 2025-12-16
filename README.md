# Project overview
A lightweight Python honeypot to capture, log, and analyze malicious network activity for educational and security research.  
Built by **Frankelly Cordero** and **Humberto Severino** from the *Central University of the East*.

---

## Goals and scope
- **Educational focus:** Provide a safe environment to observe attack behavior and learn network security fundamentals.
- **Lightweight design:** Minimal dependencies, easy to deploy on a single host or lab VM.
- **Structured telemetry:** Normalized logs ready for analysis and visualization.
- **Extensible modules:** Simple handlers for common protocols you can expand over time.

---

## Core features
- **Service emulation:** Basic listeners for TCP (e.g., SSH banner, HTTP stub, Telnet prompt) with configurable ports.
- **Request capture:** Raw bytes, parsed metadata (IP, port, timestamp), and simple protocol fields where applicable.
- **Adaptive banners:** Rotate or randomize service fingerprints to invite interaction without real access.
- **Safe responses:** Non-interactive, no privileged operations—just enough to keep an attacker talking.
- **Logging pipeline:** JSON and CSV outputs, rolling files, and optional Syslog integration.
- **Threat hints:** Basic heuristics on payloads (e.g., credential spray patterns, common exploit strings).

---

## Architecture
- **Listener layer:** Async sockets per port with lightweight protocol stubs.
- **Parser layer:** Extracts request metadata and attempts simple protocol parsing.
- **Storage layer:** Writes events to structured logs and tags sessions with IDs.
- **Analysis hooks:** Pluggable callbacks for enrichment (GeoIP, ASN, reputation feeds) and dashboards.

---

## Quick start

### 1. Install dependencies
- **Python:** 3.10+
- **Packages:** `uvloop` (Linux/macOS), `aiofiles`, `python-dotenv`, `orjson`
- **Optional:** `geoip2`, `matplotlib`, `pandas` for analysis

### 2. Environment setup
Config file: `.env` or `config.yaml`

```yaml
HONEYPORTS=22,23,80
LOG_DIR=./logs
BIND_ADDR=0.0.0.0   # use with caution
MAX_CONN_PER_MIN=200

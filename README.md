# 🛡️ NIDS — East Africa Network Intrusion Detection System
### Final Year Project | Cybersecurity | ML-Powered

---

## Project Overview

An adaptive **Network Intrusion Detection & Auto-Response System** optimized
for East African network environments. Uses Machine Learning to detect attacks
in real-time and automatically blocks malicious IPs via iptables.

---

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│                   NIDS SYSTEM                       │
│                                                     │
│  [Phase 1]        [Phase 2]        [Phase 3]        │
│  ML Model    →    Packet       →   Auto-Response    │
│  Training         Capture          Engine           │
│                      ↓                              │
│               [Phase 4]                             │
│               Web Dashboard (real-time)             │
└─────────────────────────────────────────────────────┘
```

---

## Project Files

| File                    | Description                              |
|-------------------------|------------------------------------------|
| `nids_ml_model.py`      | Phase 1: ML model training & evaluation  |
| `nids_capture.py`       | Phase 2: Live packet capture engine      |
| `nids_autoresponse.py`  | Phase 3: Auto-response (IP blocking)     |
| `nids_dashboard.py`     | Phase 4: Real-time web dashboard         |
| `requirements.txt`      | Python dependencies                      |

---

## Setup & Installation

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Prepare Dataset
```bash
mkdir data models logs
# Place your CICIDS CSV file in /data/
cp your_file.csv data/cicids2017.csv
```

### 3. Train the ML Model (Phase 1)
```bash
python nids_ml_model.py
# This creates trained models in /models/
```

### 4. Run the Full System

**Option A — Full NIDS (capture + auto-block):**
```bash
# Find your network interface
ip a

# Run with sudo (needs raw packet access + iptables)
sudo python nids_autoresponse.py eth0
```

**Option B — Dashboard only (demo mode):**
```bash
pip install flask flask-socketio
python nids_dashboard.py
# Open http://localhost:5000
```

---

## Key Features

### ✅ Phase 1 — ML Detection
- Trains Random Forest + XGBoost classifiers
- Detects: DDoS, PortScan, BruteForce, DoS, Bot, Infiltration
- Explainable AI with SHAP (shows *why* it flagged an attack)
- 95%+ accuracy on CICIDS dataset

### ✅ Phase 2 — Packet Capture
- Real-time packet sniffing with Scapy
- Extracts 80+ CICIDS-compatible flow features
- Handles hundreds of simultaneous network flows
- Multithreaded — capture and analysis run in parallel

### ✅ Phase 3 — Auto-Response
- Automatically blocks malicious IPs via iptables
- Smart decision logic:
  - >90% confidence → instant block
  - >70% confidence → rate limit → block after 3 attacks
  - <70% confidence → monitor only
- Whitelist protection (never blocks trusted IPs)
- Auto-unblock after configurable timeout (default: 60 min)
- Full audit trail in JSON

### ✅ Phase 4 — Web Dashboard
- Real-time traffic monitoring chart
- Live attack alert feed
- Attack type breakdown (donut chart)
- Blocked IPs management (with manual unblock)
- WebSocket powered (updates every second)

---

## Attack Types Detected

| Attack           | Description                              |
|------------------|------------------------------------------|
| DDoS             | Distributed Denial of Service            |
| DoS Hulk         | HTTP-based DoS attack                    |
| PortScan         | Network reconnaissance                   |
| BruteForce       | Password/auth cracking attempts          |
| Bot              | Botnet traffic                           |
| Infiltration     | Internal network infiltration            |

---

## East Africa Context (What Makes It Unique)

- Trained/tested with East African network traffic patterns in mind
- Handles mobile-dominant traffic (3G/4G heavy)
- Low-bandwidth optimized (works on limited resources)
- Relevant to local ISPs: Airtel, Vodacom, TTCL, Safaricom
- Addresses mobile money (M-Pesa) traffic safely via whitelist

---

## Tech Stack

| Layer         | Technology                          |
|---------------|-------------------------------------|
| ML            | Scikit-learn, XGBoost, SHAP         |
| Packet Capture| Scapy, PyShark                      |
| Firewall      | iptables (Linux)                    |
| Backend       | Flask, Flask-SocketIO               |
| Frontend      | HTML5, Chart.js, Socket.IO          |
| Data          | CICIDS 2017/2018 Dataset            |

---

## Team
> Final Year Cybersecurity Project
> Built with ❤️ for East African network security

---
*"Protecting East African networks — one packet at a time."*

# FRMCS Pioneer Stack

[![GitHub](https://img.shields.io/badge/GitHub-shariquetelco-black?logo=github)](https://github.com/shariquetelco)
[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.135-009688?logo=fastapi)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)](https://react.dev)
[![5G](https://img.shields.io/badge/5G-FRMCS-orange)](https://uic.org)
[![IEEE](https://img.shields.io/badge/Target-IEEE%20VTC%202026-blue)](https://vtc2026.ieee-vts.org)
[![IABG](https://img.shields.io/badge/IABG-mbH-darkblue)](https://iabg.de)

**Author:** Ahmad Sharique · IABG mbH  
**Target:** IEEE VTC 2026  
**Status:** Active Research

| Episode 1 | Episode 2 | Episode 3 |
|:---------:|:---------:|:---------:|
| ![RailGuard-PKI](https://raw.githubusercontent.com/shariquetelco/RailGuard-PKI/main/assets/images/logo.png) | ![RailThreat](https://raw.githubusercontent.com/shariquetelco/RailThreat-FRMCS-LAB/main/logo.png) | ![RAIL-IQ](https://raw.githubusercontent.com/shariquetelco/FRMCS-RAIL-IQ/main/diagrams/logo.png) |
| [RailGuard-PKI](https://github.com/shariquetelco/RailGuard-PKI) | [RailThreat-FRMCS-LAB](https://github.com/shariquetelco/RailThreat-FRMCS-LAB) | [FRMCS-RAIL-IQ](https://github.com/shariquetelco/FRMCS-RAIL-IQ) |

---

> An open, cross-layer security research testbed for the  
> **Future Railway Mobile Communication System (FRMCS)**  
> built on the Munich–Augsburg Deutsche Bahn corridor.

---

## What Is FRMCS

FRMCS is the 5G-based successor to GSM-R — the global standard for railway radio communication. It is being deployed across Europe by Deutsche Bahn, SNCF, Network Rail, and others. Security, resilience, and identity management are critical unsolved challenges at the intersection of 5G, mission-critical communications, and railway operations.

This stack is the only open-source, end-to-end FRMCS security simulation covering detection, orchestration, identity, RF validation, kernel security, post-quantum cryptography, and satellite failover in a single connected system.

---

## The Stack — 7 Episodes
```
RF Attack on FRMCS Tower
         ↓
Episode 2 — RailThreat-FRMCS-LAB
ML classifier detects jamming / spoofing / replay
         ↓
Episode 3 — FRMCS-RAIL-IQ
Corridor risk engine propagates threat across 10 towers
Fires response actions downstream
         ↓
Episode 1 — RailGuard-PKI
PKI pauses AT issuance on compromised tower
         ↓
Episode 7 — FRMCS-NTN-Failover
Satellite link activated when terrestrial corridor fails
```

| # | Project | Role | Key Tech | Status |
|---|---------|------|----------|--------|
| 1 | [RailGuard-PKI](https://github.com/shariquetelco/RailGuard-PKI) | Device identity & authorization | ECDSA-P256, ETSI TS 102941, Flask | ✅ Done |
| 2 | [RailThreat-FRMCS-LAB](https://github.com/shariquetelco/RailThreat-FRMCS-LAB) | RF + RAN threat detection | FastAPI, 11-feature ML classifier, Prometheus, Grafana | ✅ Done |
| 3 | [FRMCS-RAIL-IQ](https://github.com/shariquetelco/FRMCS-RAIL-IQ) | Corridor risk orchestration | FastAPI, Risk Engine, React | ✅ Done |
| 4 | FRMCS-RF-Corridor | Real SDR testbed | OAI, Open5GS, GNU Radio, NVIDIA Sionna | 📋 Planned |
| 5 | FRMCS-eBPF-Shield | Kernel packet anomaly detection | eBPF/XDP, bcc, libbpf, Prometheus | 📋 Planned |
| 6 | PQC-RailGuard | Post-quantum cryptography | ML-KEM (Kyber), ML-DSA (Dilithium), liboqs | 📋 Planned |
| 7 | FRMCS-NTN-Failover | Terrestrial → satellite failover | OAI NTN n254, GEO/LEO simulators | 🟡 Partial |

---

## System Architecture
```
┌─────────────────────────────────────────────────────────┐
│                  FRMCS Pioneer Stack                     │
│                                                          │
│  ┌──────────────┐    ┌──────────────┐    ┌───────────┐  │
│  │  RailThreat  │───▶│  FRMCS-      │───▶│ RailGuard │  │
│  │  Episode 2   │    │  RAIL-IQ     │    │ PKI Ep.1  │  │
│  │  Detection   │    │  Episode 3   │    │ Action    │  │
│  └──────────────┘    │  Orchestration    └───────────┘  │
│                      └──────┬───────┘                   │
│                             │                           │
│                      ┌──────▼───────┐                   │
│                      │ NTN Failover │                   │
│                      │  Episode 7   │                   │
│                      └──────────────┘                   │
└─────────────────────────────────────────────────────────┘

Munich ──T1──T2──T3──T4──T5──T6──T7──T8──T9──T10── Augsburg
              60km · 10 FRMCS towers · Deutsche Bahn corridor
```

---

## Episode Details

### Episode 1 — RailGuard-PKI
**Repository:** [RailGuard-PKI](https://github.com/shariquetelco/RailGuard-PKI)

PKI-based device identity and authorization engine for FRMCS.  
Implements ETSI TS 102941 Authorization Ticket (AT) issuance using ECDSA-P256.  
Includes NOC dashboard and Rail-AA terminal with BroadcastChannel API sync.
```
Key tech: ECDSA-P256 · ECIES · HKDF-SHA256 · ETSI TS 102941 · Flask
```

---

### Episode 2 — RailThreat-FRMCS-LAB
**Repository:** [RailThreat-FRMCS-LAB](https://github.com/shariquetelco/RailThreat-FRMCS-LAB)

RF and RAN threat detection engine for FRMCS base stations.  
11-feature Physical Layer Security + RAN fusion classifier.  
Detects jamming, spoofing, and replay attacks with confidence scoring.  
Prometheus + Grafana observability stack included.
```
Key tech: FastAPI · scikit-learn · 11-feature PLS+RAN fusion · Prometheus · Grafana
```

---

### Episode 3 — FRMCS-RAIL-IQ
**Repository:** [FRMCS-RAIL-IQ](https://github.com/shariquetelco/FRMCS-RAIL-IQ)

Corridor-level risk orchestration engine.  
Consumes threat events from RailThreat, models adjacency risk propagation across  
all 10 Munich–Augsburg towers, and fires deterministic response actions downstream  
to RailGuard-PKI and the NTN layer.
```
Key tech: FastAPI · Adjacency risk model · React · Leaflet · 
```

**Demo:**
- AUTO SIM fires 6 attack scenarios: jamming, spoofing, replay at varying confidence
- Live corridor heatmap: towers flip GREEN → YELLOW → RED in real time
- PKI pause, handover preparation, NTN standby all visible on dashboard
- Full event audit trail exported as incident report

---

### Episodes 4–7 — Planned

| Episode | Focus |
|---------|-------|
| 4 — FRMCS-RF-Corridor | Real USRP X310/B210 SDR testbed validating Sionna digital twin against measured RF |
| 5 — FRMCS-eBPF-Shield | Kernel-level packet anomaly detection combining eBPF/XDP with RF KPIs from Episode 2 |
| 6 — PQC-RailGuard | Post-quantum rekeying under degraded RF — Kyber + Dilithium replacing ECDSA-P256 |
| 7 — FRMCS-NTN-Failover | Terrestrial → satellite failover triggered by Episode 3 orchestration layer |

---

## Research Motivation

GSM-R is being replaced by FRMCS across Europe. The transition window (2025–2035) is a critical security gap — new attack surfaces are introduced before mature defenses exist. This stack provides:

- A working simulation of the full FRMCS threat lifecycle
- Open reference architecture for railway 5G security research  
- Reproducible demo environment for academic publication
- Cross-layer evidence from RF through application layer

No existing open-source project covers this full stack.

---

## How to Run Each Episode

**Episode 1 — RailGuard-PKI**
```bash
git clone https://github.com/shariquetelco/RailGuard-PKI
cd RailGuard-PKI
# See README for setup
```

**Episode 2 — RailThreat-FRMCS-LAB**
```bash
git clone https://github.com/shariquetelco/RailThreat-FRMCS-LAB
cd RailThreat-FRMCS-LAB
# See README for setup
```

**Episode 3 — FRMCS-RAIL-IQ**
```bash
git clone https://github.com/shariquetelco/FRMCS-RAIL-IQ
# Terminal 1
cd FRMCS-RAIL-IQ/backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8003
# Terminal 2
cd FRMCS-RAIL-IQ/dashboard
npm install && npm start
# Browser: http://localhost:3000
```

---

## Academic Context

Targeting **IEEE VTC 2026**.

The stack demonstrates a complete cross-layer FRMCS security architecture:
```
RF attack → ML detection → corridor orchestration → PKI action → satellite failover
```

This is the first open system connecting all five layers in a single reproducible testbed.

---

## Topics

`frmcs` `5g-railway` `railway-security` `mission-critical-communications`  
`network-orchestration` `pki` `threat-detection` `post-quantum-cryptography`  
`ntn` `satellite-failover` `ebpf` `open5gs` `deutsche-bahn` `gsm-r`

---

## License

Research and demonstration purposes.  
© 2026 Ahmad Sharique · IABG mbH · All rights reserved.

IPR notice: consult IABG IP department before external publication.
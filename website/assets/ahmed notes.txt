# 5G Network Slice Security — Research Notes

## Reference Papers & Resources
- **Primary Reference Paper**: MDPI Sensors 2025, *Cross-Layer Security for 5G/6G Network Slices*: [https://www.mdpi.com/1424-8220/25/11/3335](https://www.mdpi.com/1424-8220/25/11/3335)
- **Side-Channel Attack Reference**: [Wikipedia - Side-channel attack](https://en.wikipedia.org/wiki/Side-channel_attack)

---

## Common Attack Vectors in 5G Slicing
1. **Side-Channel Attacks**:
   Observing microarchitectural contention on shared resources (such as cache lines and the CPU ring interconnect) to extract sensitive cross-slice information or timing leaks.
2. **Resource Exhaustion (Denial of Service)**:
   Overwhelming shared hypervisor resources (vCPU, memory buffers, queue depths) to induce latency spikes and dropped packets in mission-critical slices (URLLC).
3. **Identity Deception & Spoofing**:
   Exploiting authentication gaps in PDU sessions or GTP-U tunnels to inject spoofed control/data plane traffic.

---

## Defensive Countermeasures
- **Robust Isolation**: Hardware-assisted virtualization isolation, strict SLA quotas, and dedicated virtual network function (VNF) boundaries.
- **AI-Driven Anomaly Detection**: Real-time multi-model ML inspection combining supervised classification (XGBoost) with unsupervised anomaly detection (Isolation Forest).
- **Zero-Trust Inter-Slice Architecture**: Strict verification for all intra-slice and inter-slice signaling over the 5G Service-Based Architecture (SBA).
- **Blockchain / Decentralized Authentication**: Immutable verification and logging across multi-tenant slice domains.

---

## Multi-Plane Security Architecture
- **Data Plane (Deep Packet Inspection & Flow Telemetry)**:
  ML models inspect per-PDU session statistics at the User Plane Function (UPF) in real time to spot volumetric spikes and degraded QoS.
- **Control Plane (SDN + AI Analytics / NWDAF)**:
  The 5G core analytics controller monitors global routing and signaling. When suspicious patterns emerge across slice boundaries, it instructs the Session Management Function (SMF) to terminate rogue sessions dynamically.
- **Management Plane (NFV Orchestration)**:
  Utilizes NFV Orchestration (NFVO) to instantiate on-demand virtual firewalls, apply strict hypervisor caging, or reroute critical slice traffic.

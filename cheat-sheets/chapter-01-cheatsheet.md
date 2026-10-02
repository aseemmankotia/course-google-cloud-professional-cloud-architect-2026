# Chapter 1 Cheat Sheet — The Four Case Studies

## Quick ID Table

| Case Study | Core Domain | Key Business Driver | Key Technical Requirement | Primary Trap |
|---|---|---|---|---|
| **EHR Healthcare** | Hybrid healthcare SaaS | Reduce cost, improve reliability, automate ops | Multi-cloud (GCP+AWS+on-prem), encrypt at rest & in transit, legacy API compatibility | Answers that drop AWS or on-prem connectivity entirely |
| **Helicopter Racing League (HRL)** | Live global media streaming | Grow global audience, real-time race predictions | Global low latency (CDN), 99.99% HA, ML telemetry predictions | Single-region streaming or ignoring CDN caching |
| **Mountkirk Games** | Mobile multiplayer gaming | Global launch at massive scale, low ops overhead | GKE regional clusters, global LB, real-time analytics, zero-downtime deploys | Zonal-only clusters or manual scaling answers |
| **TerramEarth** | IoT / connected vehicles | Cut unplanned downtime, boost parts/service sales | Streaming ingestion (Pub/Sub+Dataflow) for 2M vehicles, ~50TB/day | Batch-upload answers when 'near real time' is stated |

## Requirement Translation Cheat Sheet

| Executive Statement | Hidden Technical Requirement |
|---|---|
| "Know what's happening in near real time" | Streaming pipeline (Pub/Sub → Dataflow), not batch |
| "Lowest cost possible" | Optimize within existing HA/SLA constraints — not a license to violate them |
| "No single point of failure" | Multi-zone/multi-region + redundant connectivity (HA VPN 2-tunnel or Interconnect) |
| "Works with our existing systems" | Preserve legacy API/protocol compatibility, hybrid connectivity |
| "Global users, minimal delay" | Cloud CDN / global load balancing / regional backend placement |
| "Comply with regulations" | Encryption at rest & in transit, audit logging, data residency |

## Key Numbers

| Metric | Value | Notes |
|---|---|---|
| HRL target availability | 99.99% | Requires redundant, multi-region HA design |
| HA VPN SLA-qualifying topology | 2 tunnels, 2 peer gateways | Single tunnel never qualifies for 99.99% |
| TerramEarth vehicles | ~2,000,000 | Drives Pub/Sub-scale ingestion design |
| TerramEarth sensors/vehicle | 200-500, at 120-200 pts/sec | Signals streaming, not batch |
| TerramEarth new daily data | ~50TB/day | Target state after redesign |
| TerramEarth legacy upload | ~9GB/vehicle every 3 months | Current-state batch pain point |

## RTO vs RPO
- **RTO** = time to restore service after failure
- **RPO** = max acceptable data loss (in time)
- Case-study phrasing "resume within X, lose no more than Y of data" → RTO=X, RPO=Y

## Trade-off Priority Rule
Explicit numeric HA/SLA/compliance requirements = **hard constraints**.
Cost/efficiency statements = **optimization goals within those constraints**, never a reason to break the HA/SLA/compliance requirement.

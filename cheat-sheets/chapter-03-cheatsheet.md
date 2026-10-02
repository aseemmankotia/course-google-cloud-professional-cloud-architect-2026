## Chapter 3 Cheat Sheet — Networking, Multi-Region HA & DR

### VPC Design
| Feature | Shared VPC | VPC Peering |
|---|---|---|
| Admin model | Centralized (host project) | Decentralized (each VPC own admin) |
| Transitivity | N/A — all service projects share host's network | Non-transitive |
| Use case | Multiple teams/projects, one network team | Connecting independently owned VPCs |
| Firewall rules | Centrally managed in host project | Managed separately per VPC |
| Overlapping IP ranges | Not allowed within Shared VPC | Not allowed between peered VPCs |

**Private Google Access**: enable per-subnet so VMs with no external IP can reach Google APIs (Cloud Storage, BigQuery, etc.). Command: `gcloud compute networks subnets update SUBNET --region=REGION --enable-private-ip-google-access`.

### Hybrid Connectivity
| Option | Bandwidth | SLA | When to use |
|---|---|---|---|
| Dedicated Interconnect | 10 Gbps or 100 Gbps/circuit | 99.9%–99.99% (redundant) | You're in a Google colocation facility, need steady high bandwidth, avoid internet |
| Partner Interconnect | 50 Mbps–50 Gbps | 99.9%–99.99% (redundant) | Not colocated with Google — partner extends connection |
| HA VPN | up to 3 Gbps/tunnel | 99.99% (2 interfaces, redundant peer) | Encrypted connectivity over internet, lower setup time/cost |
| Classic VPN | up to 3 Gbps/tunnel | 99.9% | Legacy only — prefer HA VPN for new designs |

### Cloud Load Balancing
| Type | Scope | Layer | Internet-facing? |
|---|---|---|---|
| Global external Application LB | Multi-region, anycast IP | L7 (HTTP/S) | Yes |
| Regional external Application LB | Single region | L7 | Yes |
| Regional internal Application LB | Single region/VPC | L7 | No |
| Internal passthrough TCP/UDP LB | Single region/VPC | L4 | No |
| External passthrough Network LB | Single region | L4 | Yes |

### Cloud DNS for Hybrid/Multi-Region
- **Forwarding zone**: GCP → on-prem DNS resolution.
- **Peering zone**: let one VPC resolve another VPC's private zone (e.g., Shared VPC service projects resolving host project zone).
- **Private zone**: internal-only name resolution scoped to attached VPCs.

### Multi-Region Live Streaming Pattern (HRL)
Global external Application LB + Cloud CDN → regional backend services (MIGs) in each target region → health checks drive automatic failover to nearest healthy region.

### Top Exam Traps
1. Assuming VPC Peering is transitive (it never is).
2. Choosing Cloud VPN when the scenario clearly implies existing colocation + high steady bandwidth (should be Dedicated Interconnect).
3. Forgetting HA VPN needs **two interfaces to a redundant peer gateway** for the 99.99% SLA — a single tunnel doesn't qualify.
4. Picking a Regional LB for a 'global users, lowest latency' requirement instead of the Global external Application LB + CDN.

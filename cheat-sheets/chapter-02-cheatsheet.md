## Chapter 2 Cheat Sheet — Compute Selection & Migration Strategy

### Compute Decision Tree
| Need | Choose |
|---|---|
| Full OS/infra control, custom kernels, licensing | Compute Engine (+ MIG for scale) |
| Container orchestration, custom networking/scheduling | GKE Standard |
| Containers, no node ops, per-pod billing | GKE Autopilot |
| Stateless container, request-driven, scale-to-zero | Cloud Run |
| Simple app, integrated services, no containers needed | App Engine Standard |
| Event-driven single-purpose function | Cloud Functions (2nd gen) |

### Key Limits
| Service | Limit |
|---|---|
| Cloud Run | Max timeout: 60 min; Max concurrency: 1000/instance; scales to zero |
| Cloud Functions (2nd gen) | Built on Cloud Run; supports long timeouts for HTTP triggers |
| MIG Autoscaler | Default cooldown: 60s; default target CPU: 60% (configurable) |
| GKE Autopilot | Billed per pod request; no node management |

### Migration Strategy Mapping (6 R's)
| Scenario Keyword | Strategy |
|---|---|
| "minimal code changes", "tight deadline" | Rehost — Migrate to Virtual Machines |
| "move DB to managed service", "small optimization" | Replatform |
| "redesign for independent scaling", "microservices" | Refactor / Re-architect |
| "discontinue legacy app" | Retire |
| "keep on-prem for compliance" | Retain |

### Case Study Quick Reference
- **EHR Healthcare**: On-prem VMware + SQL Server/MySQL + HIPAA compliance + hybrid connectivity → Migrate to Virtual Machines (rehost) for VMs; Database Migration Service for SQL Server/MySQL with minimal downtime.
- **Mountkirk Games**: Monolithic game backend needing global low-latency scaling → Re-architect into microservices on GKE (regional clusters + global load balancing); independent scaling per component (matchmaking, leaderboard, chat).

### GKE Autopilot vs Standard
| Factor | Autopilot | Standard |
|---|---|---|
| Node management | Google-managed | Customer-managed |
| Billing | Per-pod resource request | Per-node (VM) |
| Control | Restricted (no privileged pods) | Full control |
| Best for | Simplicity, variable workloads | Custom infra, specialized scheduling |

### Common Exam Traps
- Choosing GKE when Cloud Run's scale-to-zero + simplicity better fits a stateless HTTP scenario.
- Confusing rehost (VM lift-and-shift) with replatform (minor managed-service swap) in migration wording.
- Assuming MIG autoscaling reacts instantly — remember the cooldown period delays scale decisions using fresh instance metrics.
- Picking Cloud Storage Transfer Service or BigQuery Data Transfer Service for operational DB migration instead of Database Migration Service.

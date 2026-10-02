## Chapter 5 Cheat Sheet: Storage & Data Solutions

### Database Selection Matrix
| Requirement | Service |
|---|---|
| Regional relational, HA failover, <64TB | Cloud SQL |
| Global relational, horizontal scale, ACID, SQL | Cloud Spanner |
| High-throughput time-series/IoT, wide-column NoSQL | Bigtable |
| Petabyte-scale SQL analytics, serverless, dashboards | BigQuery |
| Mobile/web document DB, offline sync, real-time listeners | Firestore |

### Key SLAs & Limits
| Service | Config | SLA / Limit |
|---|---|---|
| Cloud SQL | HA (regional) | Synchronous standby in different zone; max 64TB |
| Spanner | Regional | 99.99% SLA |
| Spanner | Multi-region | 99.999% SLA; min 100 processing units |
| Bigtable | Single-cluster | 99.9% SLA |
| Bigtable | Multi-cluster | 99.999% SLA |
| Pub/Sub | Retention | Default 7 days, max 31 days |

### Pub/Sub & Dataflow Streaming Pattern
```
Vehicles/IoT → Pub/Sub topic (at-least-once, ordering key = device ID)
           → Dataflow (Apache Beam): window, dedupe, transform
           → BigQuery (analytics) or Bigtable (serving layer)
```
- **Ordering**: enable message ordering + ordering key per entity (no native FIFO topic type — AWS-only concept).
- **Exactly-once processing**: handle dedup in Dataflow (Pub/Sub subscription 'exactly-once delivery' feature also available, distinct from ordering).
- **Windowing**: Fixed windows for periodic aggregates; Session windows for activity-gap grouping; Sliding for overlapping metrics. Always set 'allowed lateness' for real-world late data.

### Cloud Storage Class & Lifecycle Rules
| Class | Min Duration | Access Pattern |
|---|---|---|
| Standard | none | Frequent (daily) |
| Nearline | 30 days | <1x/month |
| Coldline | 90 days | <1x/quarter |
| Archive | 365 days | <1x/year |

- Lifecycle rules trigger on: object age, storage class, custom time, live/noncurrent version, number of newer versions.
- Common exam gotcha: transitioning an object out of a class before its minimum storage duration still incurs a full early-deletion charge for that duration.

### Bigtable Row-Key Rule
Avoid sequential/monotonic prefixes (raw timestamps) → hotspotting. Use salted or reversed-timestamp + entity ID keys to distribute load evenly across nodes.

### Common Exam Traps
1. Choosing Spanner for high-throughput IoT ingestion (should be Bigtable — cost & design mismatch).
2. Assuming Pub/Sub has FIFO topics (it doesn't — use ordering keys).
3. Picking Coldline/Nearline purely by 'cheap' without matching stated access frequency exactly.

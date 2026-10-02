## Chapter 5: Storage & Data Solutions Provisioning — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Cloud SQL max storage capacity per instance? | Up to 64TB. Exam tip: beyond this, or beyond single-region needs, move to Spanner. |
| 2 | Cloud SQL HA failover mechanism? | Synchronous replication to a standby instance in a different zone of the same region; automatic failover on primary failure. Exam tip: it's regional, not cross-region — Spanner is for cross-region HA. |
| 3 | Cloud Spanner minimum compute unit and its scaling name? | Processing Units (PU); minimum 100 PU, 1000 PU = 1 node equivalent. Exam tip: PUs let you provision fractional-node capacity for smaller workloads. |
| 4 | Cloud Spanner SLA: regional vs multi-region config? | Regional = 99.99%; multi-region = 99.999%. Exam tip: exam differentiates these two SLA tiers when asking which config meets an availability requirement. |
| 5 | Bigtable SLA: single-cluster vs multi-cluster routing? | Single-cluster = 99.9%; multi-cluster (replicated) = 99.999%. Exam tip: multi-cluster also enables regional failover, not just higher SLA. |
| 6 | Bigtable row-key design gotcha? | Avoid monotonically increasing keys (e.g., raw timestamps) as prefix — causes hotspotting on one node. Exam tip: use salting/hashing or reverse timestamp with entity ID prefix. |
| 7 | Pub/Sub default message retention period? | 7 days by default; configurable from 10 minutes up to 31 days. Exam tip: retention lets subscribers replay/seek to a timestamp within that window. |
| 8 | How do you guarantee per-entity ordered delivery in Pub/Sub? | Enable message ordering on the subscription and set an ordering key (e.g., device ID) on published messages. Exam tip: GCP Pub/Sub has no 'FIFO topic type' — that's an AWS SQS concept, a common exam trap. |
| 9 | Dataflow: how to handle late-arriving streaming data? | Set 'allowed lateness' on the window plus accumulation mode (discarding vs accumulating) in the trigger. Exam tip: without allowed lateness, late events past the watermark are dropped. |
| 10 | Cloud Storage class minimum storage durations? | Nearline = 30 days, Coldline = 90 days, Archive = 365 days. Exam tip: deleting/moving an object before its minimum duration incurs an early-deletion charge. |
| 11 | When to choose Nearline vs Coldline vs Archive (access frequency rule of thumb)? | Nearline: accessed <1x/month. Coldline: accessed <1x/quarter. Archive: accessed <1x/year. Exam tip: match the scenario's stated access frequency directly to the tier. |
| 12 | Typical streaming pipeline for vehicle telemetry into an analytics store? | Vehicles → Pub/Sub (ingestion, at-least-once) → Dataflow (streaming ETL/dedup/windowing) → BigQuery (analytics) or Bigtable (time-series serving). Exam tip: this exact chain is the canonical GCP streaming architecture pattern tested repeatedly. |

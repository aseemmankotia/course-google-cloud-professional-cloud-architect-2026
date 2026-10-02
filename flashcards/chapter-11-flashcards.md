## Chapter 11: SRE Practices, Observability & Disaster Recovery — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | SLO 99.9% over 30 days = allowed downtime? | 43.2 minutes (30 days × 1440 min × 0.001). Exam tip: memorize 99.9%→43.2m, 99.95%→21.6m, 99.99%→4.32m per 30-day window. |
| 2 | Error budget formula | Error budget = 100% − SLO target. Remaining budget = budget − actual downtime/errors consumed. Exhausted budget → freeze risky releases per SRE practice. |
| 3 | Cloud Logging _Required bucket retention | 400 days, NOT configurable. Stores Admin Activity, System Event, Access Transparency, and Policy Denied audit logs. |
| 4 | Cloud Logging _Default bucket retention | 30 days by default; configurable from 1 to 3650 days for _Default and any user-defined log bucket. |
| 5 | Blue-green vs Canary vs Rolling deployment | Blue-green: instant full cutover, needs 2x infra, instant rollback. Canary: gradual % traffic shift with metric monitoring, moderate rollback speed. Rolling: incremental instance replacement, no extra capacity, slowest full rollback. |
| 6 | DR pattern: Pilot Light | Only core components (e.g., DB replica) run continuously; rest of stack provisioned/scaled at failover time. Medium RTO/RPO, low-to-medium cost. |
| 7 | DR pattern: Warm Standby | Scaled-down but fully functional replica environment runs continuously; scaled up on failover. Lower RTO/RPO than pilot light, higher cost. |
| 8 | DR pattern: Multi-region Active-Active | All regions actively serve live traffic simultaneously with continuous replication. Near-zero RTO/RPO, highest cost and operational complexity. |
| 9 | RTO vs RPO | RTO = max acceptable time to restore service after an outage. RPO = max acceptable data loss window. Exam tip: backup/restore = highest RTO & RPO; active-active = lowest. |
| 10 | Cloud Trace default sampling | Approximately 1 sample per second per project by default (adaptive/configurable). Used to visualize per-request latency as a waterfall of spans across services. |
| 11 | Error Reporting data source | Automatically parses and groups stack traces from Cloud Logging, App Engine, GKE, GCE, Cloud Functions, and Cloud Run — no extra instrumentation needed for supported logging formats/languages. |
| 12 | Log-based metric types | Counter metric: counts matching log entries. Distribution metric: extracts a numeric field (e.g., latency) into a histogram. Exam tip: use distribution + alerting policy for percentile-based (e.g., p99) alerts. |

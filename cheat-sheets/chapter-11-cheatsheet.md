## Chapter 11 Cheat Sheet — SRE, Observability & DR

### SLI / SLO / SLA
| Term | Definition |
|---|---|
| SLI | Measured metric (latency, availability, error rate) |
| SLO | Internal target/range for an SLI |
| SLA | Contractual promise to customers, usually with penalties |

### Error Budget Table (30-day window)
| SLO | Allowed downtime |
|---|---|
| 99.9% | 43.2 min |
| 99.95% | 21.6 min |
| 99.99% | 4.32 min |
| 99.999% | 0.432 min (~26s) |

Error budget = 1 − SLO. If budget is exhausted → freeze non-critical releases, prioritize reliability work.

### Cloud Operations Suite
| Tool | Purpose |
|---|---|
| Cloud Monitoring | Dashboards, uptime checks, alerting policies |
| Cloud Logging | Centralized logs, sinks, log-based metrics |
| Cloud Trace | Distributed latency tracing (waterfall/spans) |
| Error Reporting | Auto-groups exceptions/stack traces |
| Cloud Profiler | CPU/memory profiling of running code |

### Log Retention
| Bucket | Default | Configurable? |
|---|---|---|
| _Required | 400 days | No |
| _Default / custom | 30 days | Yes, 1–3650 days |

### Log-based Metrics
- **Counter**: count of matching entries (e.g., 5xx errors)
- **Distribution**: numeric value histogram (e.g., latency percentiles)

### Deployment Strategies
| Strategy | Traffic Shift | Rollback Speed | Extra Infra |
|---|---|---|---|
| Blue-green | 100% instant | Instant | Yes (2x) |
| Canary | Gradual % | Fast (halt rollout) | Minimal |
| Rolling | Incremental replace | Slow (re-roll) | None |

### DR Patterns
| Pattern | RTO | RPO | Relative Cost |
|---|---|---|---|
| Backup/Restore | Hours+ | Hours+ | $ |
| Pilot Light | Tens of min | Minutes | $$ |
| Warm Standby | Minutes | Seconds–min | $$$ |
| Multi-region Active-Active | Seconds–min | ~Zero | $$$$ |

### Key gcloud Commands
```bash
# Uptime check
gcloud monitoring uptime-checks create http my-check --uri=https://example.com

# Log-based counter metric
gcloud logging metrics create error_count \
  --description="5xx errors" \
  --log-filter='severity=ERROR AND httpRequest.status>=500'

# Log sink to BigQuery
gcloud logging sinks create my-sink bigquery.googleapis.com/projects/PROJECT/datasets/DATASET \
  --log-filter='resource.type="cloud_run_revision"'
```

### Exam Traps
- Confusing SLO target % with error budget minutes — always convert via window length.
- Assuming _Required logs are configurable (they are NOT — fixed 400 days).
- Picking canary when question demands *instant* full rollback (that's blue-green).
- Choosing backup/restore when RTO/RPO requirements are near-zero (needs active-active).

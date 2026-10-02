## Chapter 8 Cheat Sheet: SDLC, CI/CD & Troubleshooting

### SDLC Stage → GCP Tool Mapping
| Stage | Tool |
|---|---|
| Source control | Cloud Source Repositories (or GitHub/Bitbucket mirrored) |
| CI (build/test) | Cloud Build |
| Artifact storage | Artifact Registry (Container Registry shut down March 2025) |
| CD (progressive rollout) | Cloud Deploy (GKE, Cloud Run, Anthos targets) |
| Deploy-time policy enforcement | Binary Authorization |
| Observability/troubleshooting | Cloud Logging, Error Reporting, Cloud Trace, Cloud Profiler |

### Cloud Build Key Numbers
| Item | Value |
|---|---|
| Default build timeout | 10 min (600s) |
| Max configurable timeout | 24 hr (86400s) |
| Free tier | 120 build-min/day |
| Config field for timeout | `timeout: <seconds>s` in cloudbuild.yaml |

### Deployment Strategies
| Strategy | Behavior | Rollback speed | Infra cost |
|---|---|---|---|
| Rolling update | Gradually replace old pods/instances | Medium | Low |
| Canary | Shift small % traffic, monitor, then increase | Fast (small blast radius) | Low-Medium |
| Blue/Green | Instant full traffic switch between two environments | Fastest | High (2x infra) |

### Troubleshooting Toolchain
| Need | Tool |
|---|---|
| Auto-grouped errors/stack traces | Error Reporting |
| Raw log search/queries | Cloud Logging (Logs Explorer) |
| Request latency/distributed tracing | Cloud Trace |
| CPU/memory profiling | Cloud Profiler |
| ⚠️ Deprecated (shut down May 2023) | Cloud Debugger — never select on exam |

### Key Commands
```bash
# Submit a build manually
gcloud builds submit --config=cloudbuild.yaml .

# Create a build trigger on repo push
gcloud builds triggers create github \
  --repo-name=REPO --branch-pattern="^main$" \
  --build-config=cloudbuild.yaml

# Deploy a release via Cloud Deploy
gcloud deploy releases create REL_NAME \
  --delivery-pipeline=PIPELINE --region=REGION
```

### Release Management Gates
1. **Unit tests** — fail fast, run in Cloud Build first step.
2. **Integration tests** — run against staging/ephemeral env.
3. **Canary validation** — traffic %, monitor error rate/latency via Cloud Monitoring before promoting.
4. **Approval gate** (regulated environments) — manual or Binary Authorization attestation check.

### Post-Incident Review (Blameless Postmortem)
- Timeline of events (detection → mitigation → resolution)
- Root cause (systemic, not individual)
- Action items with owners and due dates
- No punitive language — psychological safety drives honest reporting

### Technical Debt vs Delivery Speed
- Extremes (halt everything / ignore debt) are wrong exam answers.
- Correct pattern: incremental repayment (fixed % sprint capacity) + feature flags for scoped delivery.

### Change Management (Regulated Environments)
- Separation of duties: build vs approve vs deploy roles
- Binary Authorization for verified image provenance
- Audit logging (Cloud Audit Logs) for all deploy actions
- Change Advisory Board (CAB) sign-off gate before production promotion

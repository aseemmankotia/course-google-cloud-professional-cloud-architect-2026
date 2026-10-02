## Chapter 10 Cheat Sheet — Programmatic Interaction & Implementation Oversight
**Exam Domain:** Managing Implementation (9–13%)

### gcloud Command Groups
| Group | Purpose | Example |
|---|---|---|
| `gcloud compute` | VMs, disks, networks, firewall | `gcloud compute instances create` |
| `gcloud container` | GKE clusters | `gcloud container clusters create` |
| `gcloud iam` | Service accounts, roles | `gcloud iam service-accounts create` |
| `gcloud services` | Enable/disable APIs | `gcloud services enable compute.googleapis.com` |
| `gcloud projects` | Project-level admin | `gcloud projects list` |

### Config Management
- `gcloud config set project <id>` — sets default project
- `gcloud config configurations create <name>` — isolated named env config
- `gcloud config configurations activate <name>` — switch context
- Exam trap: relying on a single default project across dev/stage/prod causes accidental prod changes.

### Cloud Shell Facts
| Attribute | Value |
|---|---|
| Home directory disk | 5 GB persistent |
| Session type | Ephemeral VM, temporary |
| Idle timeout | ~20 minutes |
| Best use | Ad hoc admin tasks, quick fixes, not production automation |

### Choosing Automation Tooling
| Tool | Use When |
|---|---|
| gcloud CLI / Cloud Shell | One-off, manual, ad hoc admin tasks |
| Cloud Client Libraries | Production app code, idiomatic, retries/pagination built in |
| REST/gRPC direct | Unsupported language, custom integration, fine control |
| Legacy discovery-based library (google-api-python-client) | Still works, but not the current recommendation |

### Implementation Oversight Process
1. **Design review checkpoint** — verify built environment matches approved architecture before proceeding.
2. **Testing/validation before cutover** — load test + canary/staged rollout + rollback criteria.
3. **Drift detection** — `terraform plan` (or Config Connector reconciliation) to compare live state vs. desired config; never blindly apply/delete-recreate on production without review.
4. **Handoff to ops** — deliver architecture diagrams, requirements doc, runbooks, monitoring/alerting definitions, and sign-off record.

### Common Exam Traps
- Choosing gcloud scripting for large-scale/high-volume automation instead of Cloud Client Libraries.
- Assuming Cloud Shell sessions or in-memory state persist indefinitely.
- Skipping design review checkpoints and discovering architecture drift only after an incident.
- Reconciling infrastructure drift by deleting/recreating production resources instead of reviewing a plan/diff first.
- Confusing gcloud compute vs gcloud container command scopes.

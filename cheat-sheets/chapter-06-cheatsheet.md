## Chapter 6 Cheat Sheet — IAM, Access & Resource Hierarchy

### Resource Hierarchy
```
Organization > Folder > Project > Resource
```
- IAM policy at any level = **union of allows** from that level + all ancestors.
- IAM cannot revoke an ancestor's grant → use **Organization Policy** for restrictions (deny/allow lists), not IAM.

### IAM Role Types
| Type | Scope | Example | Least Privilege? |
|---|---|---|---|
| Primitive | Whole project, broad | Owner, Editor, Viewer, Browser | No — avoid |
| Predefined | Single service, granular | roles/storage.objectAdmin | Usually yes |
| Custom | Exact permission set you choose | myCustomVmOperator | Best fit |

**Custom roles: create at Organization or Project level ONLY — not Folder.**

### Key Organization Policy Constraints
| Constraint | Purpose |
|---|---|
| `constraints/compute.vmExternalIpAccess` | Restrict/deny external IPs on VMs |
| `constraints/iam.disableServiceAccountKeyCreation` | Block creation of SA JSON keys |
| `constraints/compute.requireOsLogin` | Enforce OS Login for SSH |
| `constraints/compute.skipDefaultNetworkCreation` | Prevent default VPC auto-creation |
| `constraints/iam.allowedPolicyMemberDomains` | Restrict principal domains allowed in IAM bindings |

### Service Accounts
- Default Compute Engine SA gets `roles/editor` — **disable/replace it**.
- User-managed keys: rotate every **90 days** if unavoidable.
- Best practice: **avoid exported keys entirely** — use attached service accounts or Workload Identity.

### Workload Identity Federation for GKE
- Binds Kubernetes ServiceAccount (KSA) → Google ServiceAccount (GSA) via `roles/iam.workloadIdentityUser`.
- Pods authenticate to GCP APIs **without any exported key**.
- Exam trap: mounting a JSON key as a K8s Secret is NOT Workload Identity and still carries key-leak risk.

### IAM Conditions
- Written in **CEL (Common Expression Language)**.
- Common attributes: `request.time`, `resource.name`, `resource.type`.
- Use case: auto-expiring temporary access (e.g., `request.time < timestamp("2026-XX-XXT00:00:00Z")`).

### Folder Design Pattern (Multi-Business-Unit / Compliance)
- One folder per business unit / compliance boundary (e.g., Healthcare-HIPAA vs Marketing).
- Apply Org Policy constraints at folder level → inherited by all current & future projects.
- Avoids per-project policy drift and manual re-application.

### Common Exam Traps
1. Choosing `roles/editor` or `roles/owner` as the "simple" answer when a scoped predefined/custom role is correct.
2. Forgetting custom roles can't be created at the Folder level.
3. Using IAM to try to *restrict* an inherited grant instead of Organization Policy.
4. Picking key-based fixes (rotate/encrypt) when Workload Identity eliminates the key entirely.

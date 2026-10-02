## Chapter 4 Cheat Sheet: IaC & Automated Provisioning

### Terraform vs Deployment Manager
| Feature | Terraform | Deployment Manager |
|---|---|---|
| Language | HCL | YAML / Jinja2 / Python |
| Cloud scope | Multi-cloud (providers) | GCP only |
| State | External, self-managed (e.g., GCS backend) | Managed internally by Google |
| Locking | Yes (backend-dependent, e.g., GCS generation-based) | Not user-exposed |
| Google direction | Actively promoted (Cloud Foundation Toolkit, Config Connector) | Maintenance mode |

### Terraform State Essentials
- Backend: GCS bucket, enable **versioning** for recovery.
- Locking: GCS backend uses object generation compare-and-swap.
- **Module** = reusable resource bundle. **Workspace** = separate state instance of same config (dev/stage/prod).

### Config Connector
- Manages GCP resources via Kubernetes **CRDs**.
- **Namespaced mode**: 1 namespace → 1 GCP project (multi-tenant, recommended).
- **Cluster mode**: 1 default project cluster-wide.
- Continuously reconciles drift like any Kubernetes controller.

### Cloud Build for IaC Pipelines
| Setting | Value |
|---|---|
| Default build timeout | 600s (10 min) |
| Max build timeout | 86400s (24 hr) |
| Trigger types | push, PR, tag, manual, Pub/Sub, webhook |
- Use Pub/Sub triggers to chain cross-project pipelines (e.g., image build → terraform apply).

### Shared VPC
- **Host project**: owns VPC, subnets, firewall rules.
- **Service project**: attaches, deploys workloads into shared subnets.
- Roles: `roles/compute.xpnAdmin` (org/folder level, enables Shared VPC) vs `roles/compute.networkUser` (subnet/project level, lets service project use subnet).
- Limit: up to **100 service projects** per host project.

### Firewall Design
| Type | Priority Range | Evaluation Order |
|---|---|---|
| VPC firewall rule | 0–65535 (lower=higher priority) | After hierarchical policy (unless goto_next) |
| Hierarchical firewall policy | 0–2147483647 | Evaluated first, from org → folder → project |
- Implied rules: allow all egress, deny all ingress (lowest priority, can't be deleted, can be overridden).

### Private Google Access & Cloud NAT
- **Private Google Access**: subnet-level setting; lets no-external-IP VMs reach Google APIs only.
- **Cloud NAT**: regional, requires Cloud Router; provides internet **egress-only** for no-external-IP VMs (no unsolicited inbound).
- Default min ports/VM: 64 (configurable).
- Common combo: enable **both** when VMs need Google API access AND general internet egress.

### Exam Traps
- Confusing workspace (state) with module (code).
- Forgetting Private Google Access ≠ internet access.
- Assuming hierarchical firewall rules can always be overridden at project level (they can't, unless `goto_next`).
- Picking Deployment Manager for multi-cloud scenarios.

# Answer Key — Practice Test 2

**Q1. Correct: D**

Cloud Spanner's multi-region configurations provide synchronous replication across regions with a 99.999% availability SLA, RPO of zero, and automatic failover well under a minute — the only option here that natively satisfies both RPO=0 and sub-60-second RTO across a full regional failure.

---

**Q2. Correct: A**

Google's SLA for Dedicated Interconnect only reaches 99.99% when two connections are provisioned in different edge availability domains (ideally different metros), each with its own Cloud Router, eliminating single points of failure at the physical and routing layers.

---

**Q3. Correct: C**

Migrate to Virtual Machines is purpose-built for rapid lift-and-shift of VMware VMs to Compute Engine with minimal application changes, making it the only option that realistically meets an 8-week hard deadline while preserving the existing tightly-coupled architecture for later modernization.

---

**Q4. Correct: D**

The Compute Network User role (roles/compute.networkUser) can be granted at the subnet level in a Shared VPC host project, allowing a service project team to attach VM instances to specific subnets without granting them any ability to modify firewall rules, routes, or subnet configuration.

---

**Q5. Correct: B**

A 3-year resource-based Committed Use Discount gives the deepest possible discount (up to ~57%) on the predictable steady-state baseline, while leaving the unpredictable burst capacity on on-demand autoscaled instances preserves flexibility without a long-term commitment on capacity that isn't consistently used.

---

**Q6. Correct: C**

Database Migration Service supports Oracle as a source for continuous, change-data-capture-based migration into AlloyDB for PostgreSQL (and Cloud SQL for PostgreSQL), enabling ongoing replication until a low-downtime cutover — directly meeting the near-zero downtime and managed-destination requirements.

---

**Q7. Correct: C**

Migrate to Virtual Machines performs streaming, continuous block-level replication from the source VMware environment, and supports launching isolated 'test clone' instances in a separate network for validation without affecting the production replication stream, minimizing cutover downtime to the final delta sync.

---

**Q8. Correct: A**

Partner Interconnect lets a customer connect through a supported service provider without needing a presence in a Google colocation facility. Achieving the 99.99% SLA requires redundant connections in two different metro/edge availability domains, matching the exact production-level design pattern tested on the exam.

---

**Q9. Correct: B**

Cloud Spanner's multi-region configurations use synchronous, quorum-based replication with external strong consistency and automatic leaderless failover, giving near-zero RPO and sub-minute automatic recovery without manual intervention — exactly what strict financial transactional workloads require.

---

**Q10. Correct: D**

A 3-year resource-based Committed Use Discount locks in a specific machine type/vCPU/memory commitment and delivers the largest available discount for guaranteed, predictable long-term usage — the tradeoff being the customer pays for the committed resources regardless of actual usage, which matches the stated business requirement.

---

**Q11. Correct: C**

Shared VPC lets a central host project own the network (subnets, firewall rules, and the single Interconnect attachment) while service projects retain separate billing and IAM boundaries for each team — this is the standard pattern for centralized network governance with per-team project isolation.

---

**Q12. Correct: A**

In Shared VPC, firewall rules always live in the host project, so any admin who manages them needs a role granted on the host project. Compute Security Admin grants firewall rule management, and an IAM condition can scope that grant to resources matching a specific tag, letting Team A manage only its own rules without touching Team B's.

---

**Q13. Correct: B**

Shared VPC or Network Connectivity Center's hub-and-spoke model centralizes connectivity so that as new departments are added, they simply attach to the shared network or hub, avoiding a growing full mesh of point-to-point connections and reducing long-term operational overhead.

---

**Q14. Correct: D**

Private Google Access lets instances without external IPs reach Google APIs (like Cloud Storage) over Google's internal network path without consuming Cloud NAT resources, while Cloud NAT is required separately to allow outbound connections to non-Google internet destinations like Docker Hub. Both are needed together to satisfy the full requirement.

---

**Q15. Correct: D**

Config Connector exposes GCP resources as Kubernetes Custom Resources, letting teams manage Cloud SQL instances, Cloud Storage buckets, and other GCP services with kubectl and standard Kubernetes-native GitOps tooling, with state tracked in the Kubernetes API alongside application manifests.

---

**Q16. Correct: B**

Cloud Deploy is the managed continuous delivery service for GKE (and other runtimes) that models a pipeline of progressive targets and natively supports requiring manual approval before a release is promoted to a given target, such as production, which is exactly the described gate.

---

**Q17. Correct: A**

Google's documented Interconnect SLA tiers require two or more Dedicated Interconnect connections located in at least two different metropolitan (Interconnect) locations, along with redundant Cloud Routers, to qualify for the 99.99% availability SLA, while keeping traffic entirely off the public internet.

---

**Q18. Correct: D**

VPC Network Peering only auto-shares each network's own subnet routes by default. Routes learned dynamically via Cloud Router (from Interconnect or VPN) are custom routes and are NOT propagated across a peering connection unless you explicitly enable 'export custom routes' on the side that owns the routes (host-prod) and 'import custom routes' on the receiving side (partner-vpc). This is a documented, exam-relevant nuance distinct from basic subnet-route sharing.

---

**Q19. Correct: B**

VPC Service Controls creates a service perimeter around BigQuery (and other supported APIs) that blocks data exfiltration to resources outside the perimeter, regardless of IAM permissions. An access level scoped to the on-prem IP range allows the Interconnect-based application through while blocking copy/export to external projects.

---

**Q20. Correct: A**

Cloud EKM lets Google Cloud services call out to an external, customer-controlled key manager (including on-prem HSM-backed partners) at the time of each cryptographic operation, so the raw key material never resides inside Google Cloud infrastructure while still supporting services like BigQuery and Compute Engine.

---

**Q21. Correct: A**

constraints/compute.vmExternalIpAccess is the specific Organization Policy constraint that controls which VM instances (if any) may be assigned external IP addresses; setting it to deny-all at the org node and inheriting down enforces the requirement with no project-level override.

---

**Q22. Correct: B**

Workload Identity Federation allows an external identity provider (GitHub's OIDC issuer) to be trusted directly, so the pipeline exchanges a short-lived OIDC token for a short-lived Google Cloud credential impersonating a service account — no long-lived key is ever created, stored, or downloaded.

---

**Q23. Correct: A**

Cloud DLP provides pre-built infoType detectors (CREDIT_CARD_NUMBER, EMAIL_ADDRESS, PHONE_NUMBER, etc.) that use pattern matching, context, and checksums to find sensitive data in free text and can automatically de-identify/mask it as part of an ingestion pipeline — no custom regex required.

---

**Q24. Correct: B**

Predefined roles are curated, service-specific bundles of permissions maintained by Google that align closely to common job functions, giving finer granularity than primitive roles without the ongoing maintenance burden of managing fully custom roles for every use case — custom roles are reserved for narrow gaps predefined roles don't cover.

---

**Q25. Correct: C**

VPC Service Controls creates a security perimeter around resources so that even users/service accounts with legitimate IAM permissions cannot exfiltrate data to services or projects outside the perimeter via APIs (copy, export, etc.). Access levels let you allow specific trusted network sources — like an on-prem range reaching in via Cloud Interconnect — to access resources inside the perimeter without weakening the exfiltration protection.

---

**Q26. Correct: A**

Workload Identity Federation lets an external OIDC-compliant identity (like GitHub Actions' built-in OIDC token, scoped to specific repo/branch claims) exchange its token for short-lived GCP credentials via impersonation of a service account — no service account key is ever generated, stored, or rotated, and each exchange is tied to a specific workflow run for auditability.

---

**Q27. Correct: D**

Blameless postmortems focused on systemic contributing factors (not individual blame) with tracked action items are the standard SRE/PCA practice for continuous improvement — they surface true root causes and encourage future incident reporting rather than concealment.

---

**Q28. Correct: D**

With a small team and a defined 2-year retention need, using managed Cloud Logging sinks into BigQuery gives fast time-to-value, low operational burden, and native SQL ad hoc querying — a clear 'buy/use managed service' win given limited engineering headcount.

---

**Q29. Correct: A**

An automated CI/CD pipeline with an enforced approval gate and Binary Authorization satisfies auditable change control (every deployment is traceable and gated) while enabling much higher deployment frequency than manual quarterly reviews — directly balancing compliance and velocity.

---

**Q30. Correct: B**

Committing the stable, continuously-used baseline (20 vCPUs) locks in the discount where usage is guaranteed, while autoscaling on-demand capacity for the variable burst avoids paying for committed capacity that sits idle outside business hours — this is the standard CUD + autoscaling cost pattern tested on the exam.

---

**Q31. Correct: C**

A sustained, measured allocation of capacity to risk-prioritized technical debt alongside ongoing feature delivery is the standard approach for balancing business velocity against long-term system health — it prevents both stalled delivery and unchecked debt accumulation.

---

**Q32. Correct: B**

Per Conway's Law and the exam's explicit coverage of aligning architecture with team/org constraints, a microservices migration is unlikely to succeed if the org structure and skills remain siloed by function; the architect should address the org and skills gap alongside the technical migration plan.

---

**Q33. Correct: B**

The core mechanism of an error budget policy is that when the budget is exhausted, feature velocity is throttled and the team's priority shifts to reliability improvements until the budget recovers. This directly ties technical process (release management) to the agreed business/technical trade-off codified in the SLO.

---

**Q34. Correct: A**

Moving to a managed CI/CD service eliminates the recurring toil of patching and manual scaling, directly freeing the platform team's time to focus on delivery work, which aligns with both the stated business goal (faster time-to-market) and the hard staffing constraint (no budget for new headcount).

---

**Q35. Correct: B**

Cloud Deploy supports custom postdeploy (and predeploy) hooks that can run verification logic, such as querying a Cloud Monitoring SLO/alert condition. If the hook exits non-zero, the phase is marked failed, which — combined with Cloud Deploy's automatic rollback-on-failure configuration — prevents promotion and rolls back without manual action.

---

**Q36. Correct: D**

Config Connector installs as a Kubernetes CRD controller in GKE and continuously reconciles GCP resources defined as Kubernetes manifests, which is exactly the GitOps-style, controller-driven reconciliation model described.

---

**Q37. Correct: C**

The GCS backend for Terraform state uses object generation preconditions to implement locking automatically — when one apply is running, a second concurrent apply will fail to acquire the lock, preventing state corruption.

---

**Q38. Correct: D**

Scheduled terraform plan runs surface any drift between actual and declared state, giving early detection, while restricting IAM edit permissions on the cluster to only the automation service account enforces that all future changes must go through the pipeline — addressing both detection and prevention.

---

**Q39. Correct: C**

The --no-promote flag deploys the new version without automatically routing production traffic to it, allowing testing via the version-specific URL before manually promoting it with traffic splitting.

---

**Q40. Correct: A**

This is the standard SRE error-budget policy: when the burn rate indicates the budget will be exhausted, feature launches that add risk are paused and engineering effort shifts to reliability work until the budget recovers. This protects users while still allowing normal release velocity once risk decreases.

---

**Q41. Correct: C**

Cloud Spanner multi-region configurations use synchronous, Paxos-based replication across regions, providing near-zero RPO and automatic failover with minimal manual intervention, comfortably meeting a 5-minute RPO and 15-minute RTO with low ongoing operational burden.

---

**Q42. Correct: C**

Cloud Trace is purpose-built for distributed tracing: it captures per-request latency data as a request flows through multiple services and renders the call graph so the specific slow hop can be identified directly.

---

**Q43. Correct: A**

Error Reporting automatically aggregates and groups exceptions across App Engine, Cloud Run, GKE, and Compute Engine by analyzing stack traces, deduplicates recurring errors, and can notify when a new error group is first detected — exactly matching the requirement.

---

**Q44. Correct: C**

Without a service mesh, the standard native-Kubernetes canary pattern is to create two Deployments with identical pod labels matched by a single Service's selector. Since a Service load-balances round-robin across all matching pod endpoints, controlling the ratio of stable-to-canary replica counts (e.g., 19 stable pods and 1 canary pod) approximates the desired traffic percentage.

---

**Q45. Correct: D**

Blameless postmortems focus on identifying and fixing systemic weaknesses (e.g., lack of automated guardrails, insufficient change review enforcement) rather than assigning individual blame, since punishing individuals discourages honest reporting and doesn't prevent recurrence; the goal is durable, process-level fixes.

---


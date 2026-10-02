## Chapter 6: Identity, Access & Resource Hierarchy — Practice Questions

**Q1.** EHR Healthcare has a HIPAA-regulated clinical business unit and a non-regulated marketing business unit sharing one GCP organization. They need different compliance guardrails (e.g., stricter data residency and external IP restrictions) enforced consistently across all current and future projects in each unit. Which resource hierarchy design BEST meets this requirement?

A) Create one folder for the entire organization and apply all Org Policy constraints at the project level for each project individually
B) Create two separate GCP organizations, one per business unit, to fully isolate policies
C) Use IAM Conditions on every resource to enforce the compliance rules per business unit
D) Create separate folders per business unit (e.g., Healthcare, Marketing) and apply Org Policy constraints at each folder so they inherit to all current and future projects

<details>
<summary>Answer</summary>

**Correct: D**

Folders are the correct hierarchy layer for grouping projects by compliance boundary; Org Policy constraints set at a folder inherit automatically to all projects (present and future) beneath it, giving consistent enforcement without per-project work.

**Why the others are wrong:**
- Project-level policies require re-applying constraints on every new project — error-prone and doesn't scale
- Separate organizations lose centralized billing, IAM visibility, and shared resources — unnecessary complexity
- IAM Conditions control access grants, not organization-wide guardrails like data residency or external IP restrictions

</details>

---

**Q2.** A developer needs permission to only start and stop Compute Engine VM instances — nothing else. Which role assignment enforces least privilege?

A) roles/compute.instanceAdmin
B) roles/compute.viewer
C) roles/editor
D) A custom role containing only compute.instances.start and compute.instances.stop permissions

<details>
<summary>Answer</summary>

**Correct: D**

A custom role lets you assemble the exact minimal permission set required, satisfying least privilege precisely.

**Why the others are wrong:**
- roles/compute.instanceAdmin grants full lifecycle management (create, delete, modify) — far more than needed
- roles/compute.viewer is read-only and cannot start or stop instances
- roles/editor grants write access across nearly every GCP service — a classic exam trap for over-privilege

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Which Organization Policy constraint prevents Compute Engine VM instances from being assigned external IP addresses?

A) constraints/compute.requireOsLogin
B) constraints/compute.vmExternalIpAccess
C) constraints/iam.disableServiceAccountKeyCreation
D) constraints/compute.skipDefaultNetworkCreation

<details>
<summary>Answer</summary>

**Correct: B**

constraints/compute.vmExternalIpAccess is the specific constraint used as an allow/deny list to restrict which VMs may have external IPs — a standard guardrail exam scenario.

**Why the others are wrong:**
- requireOsLogin enforces OS Login for SSH, unrelated to external IPs
- disableServiceAccountKeyCreation blocks key creation, not networking
- skipDefaultNetworkCreation prevents the default VPC from being auto-created on new projects

</details>

---

**Q4.** GKE pods need to call Cloud Storage and BigQuery APIs. The security team mandates no exported service account keys anywhere in the cluster. Which approach BEST satisfies this requirement?

A) Export the service account's JSON key and mount it as a Kubernetes Secret in each pod
B) Enable Workload Identity Federation for GKE, binding the Kubernetes ServiceAccount to a Google service account via roles/iam.workloadIdentityUser
C) Grant the GKE node pool's default Compute Engine service account roles/editor so all pods inherit access
D) Store the service account key in Secret Manager and have pods fetch it at startup

<details>
<summary>Answer</summary>

**Correct: B**

Workload Identity Federation for GKE lets pods impersonate a Google service account through IAM token exchange — no long-lived key ever exists.

**Why the others are wrong:**
- Mounting a JSON key as a Secret still creates an exportable, long-lived credential — violates the no-keys mandate
- Granting roles/editor on the node's default SA is both key-based (attached SA still has implicit credentials) and grossly over-privileged
- Fetching a key from Secret Manager still uses an exported key — the key exists and can leak, just relocated

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** What is the fundamental difference between GCP primitive roles and predefined roles?

A) Primitive roles (Owner, Editor, Viewer, Browser) are broad, legacy roles spanning the whole project, while predefined roles are granular, Google-curated roles scoped to a specific service
B) Primitive roles can only be assigned to service accounts, while predefined roles can only be assigned to human users
C) Predefined roles must be manually created by an admin, while primitive roles are generated automatically per project
D) There is no functional difference — both terms describe the same set of roles

<details>
<summary>Answer</summary>

**Correct: A**

Primitive roles predate fine-grained IAM and grant sweeping permissions across all services; predefined roles are maintained by Google per-service (e.g., roles/storage.objectViewer) enabling least privilege.

**Why the others are wrong:**
- Both role types can be assigned to either principal type — no such restriction exists
- Predefined roles are pre-created by Google, not manually built; that description fits custom roles instead
- The two role types differ significantly in scope and are treated distinctly on the exam

</details>

---

**Q6.** An incident responder needs read access to a specific Cloud Storage bucket for exactly the next 24 hours, after which access must automatically expire. What is the BEST way to implement this?

A) Grant roles/storage.objectViewer permanently and set a calendar reminder to manually revoke it in 24 hours
B) Create a brand-new custom role scoped to expire in 24 hours
C) Add an IAM Condition to the role binding using a CEL expression based on request.time so the grant expires automatically
D) Apply an Organization Policy constraint that limits the duration of storage access

<details>
<summary>Answer</summary>

**Correct: C**

IAM Conditions use CEL expressions (e.g., request.time < timestamp(...)) to create context-aware, automatically expiring access grants — exactly built for temporary access use cases.

**Why the others are wrong:**
- Manual revocation is error-prone and not what the exam considers a robust automated control
- Custom roles define permission sets, not time-based expiration logic
- Organization Policy constraints govern resource configuration guardrails, not individual temporal access grants

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** At which levels of the GCP resource hierarchy can a custom IAM role be created?

A) Any level, including Folder
B) Organization or Project level only — not at the Folder level
C) Project level only
D) Organization level only

<details>
<summary>Answer</summary>

**Correct: B**

GCP explicitly supports custom role creation at the Organization or Project level; Folders do not support custom role definitions — a frequently tested detail.

**Why the others are wrong:**
- Folder-level custom role creation is not supported by the platform
- Project-only ignores the valid Organization-level option
- Organization-only ignores the valid Project-level option

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A security audit discovers a service account's exported JSON key committed to a public source repository. What is the BEST remediation strategy?

A) Rotate the key immediately but continue using exported keys with a 90-day rotation policy going forward
B) Migrate the workload to Workload Identity Federation to eliminate exported keys, and apply the constraints/iam.disableServiceAccountKeyCreation Org Policy to prevent recurrence
C) Encrypt the existing key using Cloud KMS before committing future versions to the repository
D) Leave the service account key as is, but restrict repository access using IAM

<details>
<summary>Answer</summary>

**Correct: B**

The root cause is reliance on long-lived exported keys; the durable fix removes the need for keys entirely (Workload Identity) and enforces the guardrail organization-wide via Org Policy so it cannot happen again.

**Why the others are wrong:**
- Continued key rotation reduces but does not eliminate the risk of key leakage — treats a symptom, not the cause
- Encrypting a key that's already exported and exposed doesn't remediate the incident or prevent recurrence
- Restricting repo access does nothing to address the leaked key's continued validity or future leaks

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---


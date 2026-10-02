## Chapter 10: Programmatic Interaction & Implementation Oversight — Practice Questions

**Q1.** An architect approves a design requiring 500 nearly-identical Compute Engine VMs to be created nightly by a CI/CD pipeline, with results parsed and fed into a downstream reconciliation service. Which approach BEST fits this automation requirement?

A) Use the Cloud Client Library for Compute Engine in the pipeline's application code
B) Write a Cloud Shell script that runs gcloud compute instances create in a loop each night
C) Have an operator manually run gcloud commands from their workstation each night
D) Use the legacy google-api-python-client discovery-based library directly

<details>
<summary>Answer</summary>

**Correct: A**

Cloud Client Libraries are idiomatic, strongly typed, handle retries/pagination/auth natively, and integrate cleanly into pipeline code that must parse structured responses — the right tool for programmatic, high-volume automation.

**Why the others are wrong:**
- gcloud in a loop works for ad hoc tasks but is fragile at scale, hard to parse reliably, and not intended as a production automation SDK
- Manual execution violates repeatability and automation requirements of the architecture
- The discovery-based client library still works but is legacy; Cloud Client Libraries are the current recommended, more maintainable choice

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Which gcloud command group is used to list, create, and manage Google Kubernetes Engine clusters?

A) gcloud compute
B) gcloud services
C) gcloud container
D) gcloud kubernetes

<details>
<summary>Answer</summary>

**Correct: C**

GKE cluster management commands live under gcloud container clusters (e.g., gcloud container clusters create).

**Why the others are wrong:**
- gcloud compute manages VMs, disks, networks — not GKE clusters
- gcloud services manages API enablement, not clusters
- gcloud kubernetes is not a valid top-level command group

</details>

---

**Q3.** An implementation engineer regularly switches between three GCP projects (dev, staging, prod) using gcloud CLI and keeps accidentally deploying to the wrong project. What is the BEST way to prevent this?

A) Log out and back in with gcloud auth login before every command
B) Always pass --project explicitly and additionally use gcloud config configurations to maintain separate named configurations per environment
C) Ask the architect to grant Owner role only on prod to prevent mistakes
D) Rely on gcloud's default project set once at install time

<details>
<summary>Answer</summary>

**Correct: B**

gcloud config configurations create <name> lets engineers maintain isolated project/account/zone settings per environment and switch with gcloud config configurations activate, and combining this with explicit --project flags is the recommended safeguard against cross-environment mistakes.

**Why the others are wrong:**
- Re-authenticating does not change which project is targeted
- Restricting roles reduces blast radius but doesn't solve the underlying tooling/process problem the exam is testing
- Relying on a single default project is exactly the practice causing the mistake

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company manages its infrastructure with Terraform. Over several months, engineers have made manual console changes to fix urgent production issues. The architect wants to detect where live infrastructure no longer matches the approved design. What should be done FIRST?

A) Delete all resources and recreate them from Terraform to guarantee consistency
B) Disable IAM permissions for console access to prevent further changes
C) Re-write the Terraform configuration to match whatever is currently deployed
D) Run terraform plan against the existing state and review the diff before taking any corrective action

<details>
<summary>Answer</summary>

**Correct: D**

terraform plan compares desired state (config) against real state (refreshed from the provider) and reports drift without making changes — the correct first step before deciding how to reconcile.

**Why the others are wrong:**
- Deleting and recreating production resources risks outages and data loss and is not the first diagnostic step
- Restricting IAM is a good longer-term control but doesn't detect existing drift
- Blindly rewriting config to match current state could bake in unapproved, non-compliant changes without review

</details>

---

**Q5.** During implementation, the architect wants to ensure a project team correctly built a multi-region deployment per the approved architecture document before go-live. Which practice BEST accomplishes this?

A) Wait until production incidents occur and use them to identify architecture deviations
B) Hold a scheduled design review checkpoint comparing the deployed environment against architecture diagrams and requirements before cutover
C) Trust the implementation team's self-reported completion status
D) Have the architect personally execute all deployment commands

<details>
<summary>Answer</summary>

**Correct: B**

Design review checkpoints are the formal mechanism architects use to validate that implementation teams have followed the approved design before production traffic is cut over, catching deviations early.

**Why the others are wrong:**
- Reactive incident-driven discovery is costly and defeats the purpose of proactive oversight
- Self-reported status without verification is not a validation control
- Architects typically don't personally execute implementation — their role is design and validation oversight

</details>

---

**Q6.** Before cutting a new payment-processing service over to production, what is the BEST validation approach to minimize risk?

A) Deploy directly to 100% of production traffic and monitor for errors
B) Run load testing and a canary/staged rollout with automated rollback criteria in a pre-production-like environment first
C) Skip testing since the architecture was already peer-reviewed on paper
D) Only test the happy-path functional scenarios manually once

<details>
<summary>Answer</summary>

**Correct: B**

Combining load/performance testing with a canary or staged rollout and defined rollback triggers validates both functional correctness and production-scale behavior while limiting blast radius — standard pre-cutover practice.

**Why the others are wrong:**
- Full production deployment without staged validation exposes all users to potential failure
- Paper design review doesn't validate actual runtime behavior or performance
- Manual happy-path-only testing misses load, failure, and edge-case behavior the exam expects you to test

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the primary purpose of a design review checkpoint in the implementation phase of the professional-cloud-architect exam framework?

A) To formally verify that what implementation teams built matches the approved architecture before proceeding to the next phase
B) To assign billing budgets to each team
C) To replace the need for automated testing
D) To grant IAM roles to new team members

<details>
<summary>Answer</summary>

**Correct: A**

Design review checkpoints exist specifically to catch architectural drift between approved design and actual build-out at defined milestones, before moving forward.

**Why the others are wrong:**
- Budget assignment is a financial governance task, not the purpose of a design review
- It complements, not replaces, automated testing
- IAM provisioning is an operational task unrelated to design validation

</details>

---

**Q8.** An engineer opens Cloud Shell to make an urgent one-off firewall rule change. After 25 minutes of inactivity mid-task, the session disconnects and the engineer loses unsaved shell variables. What should the engineer have known about Cloud Shell?

A) Cloud Shell sessions never time out
B) Cloud Shell provides a persistent 5GB home directory disk, but the VM session itself is ephemeral and disconnects after about 20 minutes of inactivity
C) Cloud Shell requires a dedicated VM to be provisioned in advance
D) All files and variables in Cloud Shell are lost immediately after each command

<details>
<summary>Answer</summary>

**Correct: B**

Cloud Shell gives each user a persistent 5GB disk mounted at $HOME that survives across sessions, but the underlying compute session is temporary and disconnects after roughly 20 minutes of inactivity, along with any in-memory shell state like variables.

**Why the others are wrong:**
- Sessions do time out after inactivity — this is a known exam trap
- Cloud Shell provisions its ephemeral VM automatically on demand, no advance setup needed
- Files in $HOME persist across sessions on the persistent disk; only session state (variables, running processes) is lost

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---


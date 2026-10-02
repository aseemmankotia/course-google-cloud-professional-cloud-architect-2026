## Chapter 8: Technical Process Optimization: SDLC, CI/CD & Troubleshooting — Practice Questions

**Q1.** A team wants an automated pipeline that builds a container on every push, pushes it to a private registry, then progressively rolls it out to GKE with automatic rollback if error rates spike. Which combination BEST meets this requirement?

A) Use Cloud Build to build/test and push the image to Artifact Registry, then use Cloud Deploy to progressively roll out with a canary strategy and automated rollback triggered by Cloud Monitoring alerts
B) Use Cloud Build to build and test, then run kubectl apply directly against the production cluster from the build step
C) Run Jenkins on a Compute Engine VM with a custom shell script that deploys via gcloud commands
D) Use Cloud Functions triggered by Pub/Sub messages to redeploy the GKE workload on every commit

<details>
<summary>Answer</summary>

**Correct: A**

Cloud Build handles CI (build/test/push to Artifact Registry) and Cloud Deploy is the managed CD service purpose-built for progressive/canary rollouts to GKE with verification gates and rollback tied to monitoring signals.

**Why the others are wrong:**
- Direct kubectl apply from a build step has no progressive rollout, verification gate, or automated rollback capability
- Self-managed Jenkins on a VM adds operational overhead and has no native integration with Cloud Monitoring for automated rollback decisions
- Cloud Functions triggered redeploys are not designed for orchestrating canary traffic shifting or rollback logic

</details>

---

**Q2.** A company is standing up a new CI/CD pipeline in 2026 and needs a private, regional repository for Docker images, npm packages, and Maven artifacts with built-in vulnerability scanning, integrated with Cloud Build triggers. Which service should they use?

A) Container Registry
B) Artifact Registry
C) A custom Docker registry hosted on Cloud Storage
D) Cloud Source Repositories

<details>
<summary>Answer</summary>

**Correct: B**

Artifact Registry is the current GCP-native artifact management service, supporting multiple formats (Docker, npm, Maven, Python, Go, Apt/Yum) with built-in vulnerability scanning and native Cloud Build integration.

**Why the others are wrong:**
- Container Registry was deprecated and shut down in March 2025; it is no longer available for new projects
- A custom registry on Cloud Storage requires building and maintaining scanning, auth, and format support manually
- Cloud Source Repositories is a Git hosting service, not an artifact/package repository

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A Cloud Build pipeline's integration test step consistently fails with a timeout error after running for 10 minutes, even though the tests need about 45 minutes to complete. What is the correct fix?

A) Increase the Cloud Build machine type to a higher CPU tier
B) Split the trigger into five separate triggers running in parallel
C) Add a `timeout` field set to a value like `3600s` at the build level in cloudbuild.yaml
D) Switch the Cloud Build region to one with higher default quotas

<details>
<summary>Answer</summary>

**Correct: C**

Cloud Build's default overall build timeout is 10 minutes (600s), configurable up to 24 hours (86400s) via the top-level `timeout` field in cloudbuild.yaml — this directly addresses a build exceeding the default duration.

**Why the others are wrong:**
- A larger machine type may speed up compute-bound steps but does not change the timeout enforcement
- Splitting into parallel triggers adds complexity and doesn't guarantee the single long-running test suite finishes within 10 minutes
- Region has no effect on per-build timeout configuration

</details>

---

**Q4.** During a production incident, users report intermittent 500 errors from a Cloud Run service. Which tool should be checked FIRST to automatically see error occurrences grouped by stack trace and spike volume, without writing custom log queries?

A) Cloud Logging Logs Explorer with a manually written filter
B) Error Reporting
C) Cloud Trace
D) Cloud Debugger

<details>
<summary>Answer</summary>

**Correct: B**

Error Reporting automatically aggregates and groups errors by stack trace signature, shows occurrence spikes over time, and can notify on new error types — ideal for a fast first-look triage.

**Why the others are wrong:**
- Logs Explorer can find the same data but requires manually constructing filters/queries instead of automatic grouping
- Cloud Trace focuses on request latency and distributed tracing, not error aggregation
- Cloud Debugger was deprecated and shut down in May 2023 and is no longer available

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A regulated healthcare company requires that only container images which passed a vulnerability scan and were signed by the CI pipeline can be deployed to their GKE clusters. Which GCP feature enforces this at deploy time?

A) Binary Authorization
B) IAM conditional policies on the deployment service account
C) VPC Service Controls
D) Organization Policy Constraints

<details>
<summary>Answer</summary>

**Correct: A**

Binary Authorization enforces deploy-time policy that only images with required attestations (e.g., passed vulnerability scan, signed by build pipeline) can be deployed to GKE or Cloud Run.

**Why the others are wrong:**
- IAM conditions control who can call an API, not whether an image has valid attestations
- VPC Service Controls establishes network/data exfiltration perimeters, not image provenance checks
- Organization Policy Constraints restrict resource configuration options, not image signature verification

</details>

---

**Q6.** What is the primary goal of a blameless postmortem process after a production incident?

A) Identify which individual engineer caused the outage so it can be documented
B) Calculate the SLA financial penalty owed to affected customers
C) Focus on systemic and process failures rather than individual fault, producing a timeline and actionable prevention items
D) Assign remediation tasks solely to the on-call engineer without broader team review

<details>
<summary>Answer</summary>

**Correct: C**

Blameless postmortems intentionally avoid attributing fault to individuals, instead analyzing systemic/process gaps and producing a timeline plus concrete action items to prevent recurrence.

**Why the others are wrong:**
- This is the opposite of blameless culture and discourages honest incident reporting in the future
- SLA penalty calculation is a contractual/business process, not the purpose of a postmortem
- Limiting review to a single individual defeats the purpose of a team-wide systemic review

</details>

---

**Q7.** A team maintains an untested legacy monolith on Compute Engine with growing technical debt, and product management wants a new feature delivered by end of quarter. As the cloud architect, what is the BEST recommendation?

A) Halt all new feature work until the entire monolith is refactored
B) Ship the feature as fast as possible with no additional tests to hit the deadline
C) Rewrite the entire service in a different language before continuing any feature work
D) Deliver a scoped minimal version of the feature behind a flag while allocating a fixed percentage of sprint capacity to incrementally pay down technical debt, tracked in the backlog

<details>
<summary>Answer</summary>

**Correct: D**

This balances delivery speed with sustainable debt reduction — an incremental, tracked approach that doesn't block business needs but prevents debt from growing unchecked.

**Why the others are wrong:**
- Halting all feature work is an extreme response disproportionate to the risk and ignores business needs
- Shipping with no tests increases technical debt further and risks additional incidents
- A full rewrite is high-risk, high-cost, and unnecessary to meet a single feature deadline

</details>

---

**Q8.** Which GCP service provides fully managed private Git repository hosting that integrates natively with Cloud Build triggers as the source stage of an SDLC pipeline?

A) Artifact Registry
B) Cloud Build
C) Cloud Deploy
D) Cloud Source Repositories

<details>
<summary>Answer</summary>

**Correct: D**

Cloud Source Repositories provides fully managed private Git repos on GCP (or can mirror GitHub/Bitbucket) and integrates directly with Cloud Build triggers for the source/CI stage of the pipeline.

**Why the others are wrong:**
- Artifact Registry stores build outputs/packages, not source code
- Cloud Build performs CI orchestration (build/test), it does not host source code repositories
- Cloud Deploy is a continuous delivery service for deployment orchestration, not source control

</details>

---


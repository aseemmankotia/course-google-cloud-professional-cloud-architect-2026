# Answer Key — Practice Test 1

**Q1. Correct: D**

Cloud SQL cross-region read replicas replicate continuously with very low lag, easily meeting a 15-minute RPO, and can be promoted to a standalone primary quickly to meet a 1-hour RTO, all while being fully managed by Google.

---

**Q2. Correct: C**

Dedicated Interconnect provides a direct physical connection between the on-premises network and Google's network at a colocation facility, supporting 10 Gbps or 100 Gbps circuits with private, predictable-latency connectivity that never touches the public internet.

---

**Q3. Correct: D**

Migrate to Virtual Machines automates a lift-and-shift of VMware VMs to Compute Engine with minimal downtime, meeting the tight 3-month deadline with low risk, while preserving the option to modernize to microservices in a later phase.

---

**Q4. Correct: D**

Shared VPC allows a central host project to own and manage the network resources (subnets, routes, firewall rules) while service projects retain their own IAM and billing separation, exactly matching the requirement for centralized network control with separate team boundaries.

---

**Q5. Correct: A**

Cloud Run natively deploys arbitrary custom container images, scales to zero automatically, and supports request timeouts of up to 60 minutes, directly satisfying all stated requirements with the lowest operational overhead.

---

**Q6. Correct: B**

A 3-year Committed Use Discount offers the deepest discount (up to roughly 70%) for predictable, long-running workloads with committed vCPU and memory usage, which matches this steady-state, non-interruptible workload.

---

**Q7. Correct: A**

A cross-region read replica continuously replicates data with minimal lag (meeting the 15-minute RPO) and can be promoted to a standalone primary quickly (meeting the 1-hour RTO), which is the standard Cloud SQL DR pattern.

---

**Q8. Correct: B**

Dedicated Interconnect provides a direct physical connection between the on-premises network and Google's network, keeps traffic off the public internet, supports circuits up to 10 Gbps (or 100 Gbps with newer offerings), and is covered by an SLA.

---

**Q9. Correct: A**

Migrate to Virtual Machines automates bulk migration of VMware VMs to Compute Engine with minimal changes to the OS or application, and can scale to migrate hundreds of VMs within a tight timeline, matching the lift-and-shift requirement.

---

**Q10. Correct: A**

A 3-year resource-based committed use discount offers the largest discount (up to roughly 55-70% depending on machine type) for workloads with predictable, stable, long-term usage where the team can commit in advance.

---

**Q11. Correct: D**

Cloud Run is a fully serverless platform with no infrastructure to manage, billed per request and execution duration, while GKE Autopilot is still a Kubernetes environment (billed per pod resource requests) that gives architects more control over networking, custom controllers, and stateful workloads that Cloud Run doesn't natively support.

---

**Q12. Correct: B**

Shared VPC lets a host project (owned by the networking team) centrally control subnets, routes, and firewall rules while service projects (owned by app teams) deploy resources into those shared subnets, giving private connectivity without granting network admin rights to app teams.

---

**Q13. Correct: B**

BigQuery is a serverless, fully managed data warehouse built for petabyte-scale SQL analytics with no infrastructure provisioning, matching the ad-hoc SQL and no-ops requirements exactly.

---

**Q14. Correct: B**

Private Google Access allows VM instances with only internal IP addresses to reach Google APIs and services (Cloud Storage, Artifact Registry, etc.) using Google's private network path instead of the public internet.

---

**Q15. Correct: A**

Dedicated Interconnect provides direct physical connections between the customer's network and Google's network at a supported colocation facility, offering high throughput (10 Gbps or 100 Gbps circuits), an SLA up to 99.99% (with redundant configurations), and private RFC 1918 connectivity without traversing the public internet.

---

**Q16. Correct: D**

Terraform is an open-source, provider-agnostic IaC tool that uses declarative HCL configuration and a state file to track resource metadata, and it supports providers for AWS, Azure, and many others in addition to Google Cloud, making it suitable for multi-cloud provisioning.

---

**Q17. Correct: A**

Cloud Build triggers integrate directly with source repositories to automatically build on push events; Artifact Registry provides integrated container vulnerability scanning on push, and a deploy step (e.g., using the Cloud Build GKE deploy step or kubectl) completes a fully automated CI/CD pipeline with no manual intervention.

---

**Q18. Correct: A**

Hierarchical firewall policies are evaluated before VPC-level firewall rules and are enforced regardless of changes made within individual VPC firewall configurations. Attaching a policy at the folder level containing prod-db, with an explicit deny-all except TCP 5432 from analytics, guarantees the restriction cannot be bypassed by future VPC-level rule changes in the host project.

---

**Q19. Correct: A**

Workload Identity (Federation) lets Kubernetes service accounts impersonate Google service accounts using short-lived, automatically rotated credentials obtained via the metadata server — no exportable JSON keys are ever created or stored, satisfying the audit requirement.

---

**Q20. Correct: A**

The gcp.resourceLocations Organization Policy constraint restricts where resources can be created across the entire org hierarchy, enforcing data residency at resource-creation time regardless of who creates it.

---

**Q21. Correct: C**

CMEK lets the customer create and control keys in Cloud KMS, set rotation schedules, and disable/destroy keys to revoke access immediately, while Google still manages the KMS infrastructure — exactly matching the described requirements.

---

**Q22. Correct: D**

VPC Service Controls creates a security perimeter around GCP resources, blocking data movement (via APIs) to services or projects outside the perimeter even by users with valid IAM permissions, which directly mitigates insider exfiltration to external projects.

---

**Q23. Correct: D**

Secret Manager is purpose-built for storing, versioning, and controlling IAM access to secrets like passwords, while Cloud DLP provides built-in infoType detectors (including CREDIT_CARD_NUMBER) to inspect and redact sensitive data in text.

---

**Q24. Correct: A**

Assigning Storage Object Viewer at the bucket level and BigQuery Data Editor at the dataset level grants only the specific read and write permissions needed, scoped to the exact resources involved, fully aligning with least privilege.

---

**Q25. Correct: C**

VPC Service Controls creates a service perimeter around GCP resources (BigQuery, Cloud Storage, etc.) that blocks data movement to services or projects outside the perimeter, even if the caller has valid IAM permissions and credentials. This directly mitigates exfiltration via compromised credentials or misconfigured IAM bindings, which is exactly the scenario described.

---

**Q26. Correct: C**

A regional Cloud KMS key ring stores keys in a specific region, satisfying the co-location/data residency requirement. Cloud KMS supports configurable automatic rotation periods, so setting it to 365 days meets the annual rotation requirement, and CMEK lets the customer retain full control over the key used to encrypt the Cloud Storage data.

---

**Q27. Correct: D**

A blameless postmortem focuses on identifying systemic root causes and generating concrete action items, which improves reliability while preserving a healthy engineering culture and encouraging future incident reporting.

---

**Q28. Correct: C**

Committed use discounts require a 1- or 3-year commitment to a specific amount of vCPU/memory or spend, and provide the largest discount (up to ~70%) for predictable, steady-state workloads.

---

**Q29. Correct: D**

Given no internal ML expertise and a need for fast time to market, using Vertex AI AutoML or a managed prebuilt API is the 'buy' option that delivers results quickly without requiring specialized in-house skills.

---

**Q30. Correct: D**

Cloud Deploy natively supports canary deployment strategies defined in the delivery pipeline configuration, allowing gradual traffic shifting and automated verification/rollback for GKE targets.

---

**Q31. Correct: B**

Continuously allocating a fixed portion of capacity each cycle to technical debt prevents it from accumulating to a point where it blocks delivery, while still allowing steady feature progress — a recommended continuous improvement practice.

---

**Q32. Correct: C**

Automating policy enforcement with policy-as-code and relying on Cloud Audit Logs for traceability satisfies compliance requirements while removing manual bottlenecks for low-risk changes, enabling faster and safer releases.

---

**Q33. Correct: B**

Blameless postmortems are the Google-recommended SRE practice: they focus on system and process gaps rather than punishing individuals, which encourages honest disclosure of root cause and produces trackable action items that drive continuous improvement.

---

**Q34. Correct: A**

Automating testing within a CI/CD pipeline directly addresses the bottleneck (manual QA) using the team's existing engineering strength, enabling smaller, more frequent, lower-risk releases and is the standard recommendation for optimizing SDLC/release management processes on the exam.

---

**Q35. Correct: B**

Terraform configs in version control give a declarative, auditable change history (via commit log) and let you roll back by reverting to a prior commit and re-applying, satisfying both requirements while remaining repeatable across projects.

---

**Q36. Correct: C**

Cloud Build is Google Cloud's CI/CD service that supports triggers on repo pushes, builds container images, and can deploy them to GKE as part of a defined build pipeline (cloudbuild.yaml).

---

**Q37. Correct: C**

Service accounts are designed for non-interactive, programmatic access. Workload identity federation lets external CI/CD systems obtain short-lived credentials without managing long-lived keys, and gcloud auth activate-service-account is the standard fallback for key-based authentication.

---

**Q38. Correct: B**

The core benefit of IaC is declaring desired state in code, storing it under version control for peer review and history, and enabling consistent, repeatable, and reversible deployments across environments.

---

**Q39. Correct: B**

Canary or blue/green deployments combined with load testing let teams validate behavior under realistic production traffic and load while limiting the blast radius if problems occur, which is the recommended safe-rollout pattern for implementation.

---

**Q40. Correct: B**

A cross-region read replica keeps a continuously updated copy of data in another region (satisfying the tight RPO), and an automated, tested promotion runbook/script can bring it online as the new primary well within a 10-minute RTO. This is the standard Cloud SQL pattern for regional DR.

---

**Q41. Correct: C**

Error Reporting automatically analyzes and aggregates application errors from logs across App Engine, GKE, Compute Engine, and Cloud Functions, grouping them by stack trace signature with no custom query configuration required.

---

**Q42. Correct: A**

30 days = 43,200 minutes. An error budget of 0.1% (100% - 99.9%) of that window is 43,200 x 0.001 = 43.2 minutes of allowed downtime.

---

**Q43. Correct: C**

Canary deployment routes a small, controlled percentage of production traffic to the new version so teams can observe real-world metrics before increasing traffic, with fast rollback by shifting traffic weight back — exactly the pattern described.

---

**Q44. Correct: C**

An SLI (e.g., request latency, error rate) is the actual measured metric. An SLO is the target or acceptable range set for that SLI (e.g., 99.9% of requests under 300ms). An SLA is the external, often contractual, commitment tied to consequences if the SLO is missed.

---

**Q45. Correct: D**

Scheduled persistent disk snapshots stored in a multi-region location are durable across regions and can be used to create a new persistent disk in any region, enabling recovery of application data in a different region during a regional outage.

---


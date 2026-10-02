## Chapter 4: Infrastructure as Code & Automated Provisioning — Practice Questions

**Q1.** A team stores Terraform state as a local file on each engineer's laptop, causing frequent 'state drift' conflicts. Which change BEST fixes this for a multi-engineer team managing GCP infrastructure?

A) Create a separate Terraform workspace for each engineer
B) Commit the local state file into the shared Git repository
C) Migrate the project to Deployment Manager instead
D) Configure a GCS backend with state locking enabled

<details>
<summary>Answer</summary>

**Correct: D**

A GCS backend centralizes state and uses the GCS object generation number to implement locking, preventing concurrent applies from corrupting state.

**Why the others are wrong:**
- Workspaces isolate state per environment, not per engineer, and don't solve the lack of a shared source of truth
- Committing binary state to Git causes merge conflicts and exposes secrets in plaintext
- Switching tools doesn't address the root cause and abandons existing Terraform investment unnecessarily

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company runs workloads on both GCP and AWS and wants a single IaC tool for both. Which factor should MOST influence choosing Terraform over Deployment Manager?

A) Terraform supports multiple cloud providers through a single HCL-based tool, while Deployment Manager only manages GCP resources
B) Deployment Manager supports YAML while Terraform does not support any templating
C) Deployment Manager provides native state locking that Terraform lacks
D) Terraform can only be executed from within Cloud Shell

<details>
<summary>Answer</summary>

**Correct: A**

Terraform's provider model lets a single configuration language manage GCP, AWS, and other providers, which is essential for multi-cloud consistency.

**Why the others are wrong:**
- Terraform fully supports HCL templating and variables; this claim is false
- Terraform (via its GCS/remote backends) supports locking; DM has no equivalent concept exposed to users
- Terraform runs from any shell, CI system, or local machine with the binary installed

</details>

---

**Q3.** A platform team wants developers to provision GCS buckets and Cloud SQL instances by submitting Kubernetes manifests through their existing GitOps pipeline, without calling GCP APIs directly. Which tool should they use?

A) Deployment Manager
B) Cloud Build alone, with no other tooling
C) A scheduled gcloud CLI script run via cron
D) Config Connector

<details>
<summary>Answer</summary>

**Correct: D**

Config Connector exposes GCP resources as Kubernetes CRDs, letting teams manage GCP infra the same way they manage workloads, fitting naturally into existing GitOps/Kubernetes pipelines.

**Why the others are wrong:**
- Deployment Manager uses YAML/Jinja2/Python templates, not Kubernetes manifests
- Cloud Build executes pipelines but has no native concept of reconciling Kubernetes CRDs to GCP resources without Config Connector
- A cron script is imperative, not declarative, and doesn't integrate with GitOps reconciliation

</details>

---

**Q4.** A Cloud Build pipeline running 'terraform apply' fails because the default build timeout is exceeded during a large deployment. Which cloudbuild.yaml field should be increased?

A) options.machineType
B) substitutions
C) availableSecrets
D) timeout

<details>
<summary>Answer</summary>

**Correct: D**

The 'timeout' field controls the maximum build duration; default is 600 seconds (10 minutes) and can be raised up to 86400 seconds (24 hours).

**Why the others are wrong:**
- machineType controls compute size/speed, not maximum duration
- substitutions define variable values for the build, unrelated to timing
- availableSecrets configures Secret Manager access, unrelated to duration

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A company has one networking team and dozens of application teams, each owning a separate GCP project. They need centralized firewall and subnet management while letting app teams deploy VMs into shared subnets. Which topology BEST meets this?

A) Give each application team its own VPC connected via VPC Peering to a hub network
B) Put all teams in a single project and use IAM conditions to separate resources
C) Connect all projects using Cloud Interconnect
D) Configure Shared VPC with a host project owned by the networking team and each application project attached as a service project

<details>
<summary>Answer</summary>

**Correct: D**

Shared VPC lets a central host project own the network and firewall rules while service projects (owned by app teams) attach and deploy resources into shared subnets, matching the centralized-network/decentralized-workload requirement exactly.

**Why the others are wrong:**
- VPC Peering doesn't provide centralized subnet/firewall administration and has transitive routing limitations
- A single project doesn't provide the resource-level isolation and billing separation app teams need
- Cloud Interconnect connects on-prem to GCP, not project-to-project within GCP

</details>

---

**Q6.** A fleet of Compute Engine VMs has no external IP addresses. They must pull container images from a public internet registry AND call Cloud Storage APIs. Which configuration is required?

A) Enable Private Google Access only
B) Configure Cloud NAT only
C) Configure Cloud NAT for internet egress AND enable Private Google Access for Google API access
D) Assign external IP addresses to all VMs

<details>
<summary>Answer</summary>

**Correct: C**

Private Google Access reaches Google APIs (like Cloud Storage) from internal IPs, but does not provide general internet access; Cloud NAT is needed for reaching the public internet registry. Both are required together for this scenario.

**Why the others are wrong:**
- Private Google Access alone can't reach a public internet registry
- Cloud NAT alone works for internet egress but Google API traffic without Private Google Access may route through the internet path unnecessarily, and some private-only configurations require it explicitly
- Assigning external IPs contradicts the stated no-external-IP requirement and increases attack surface

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** An organization admin wants to enforce a firewall rule blocking SSH from the internet across all folders and projects, overriding any allow rules created by individual project owners. Which mechanism should be used?

A) A VPC firewall rule with priority 1000 applied in each project
B) A hierarchical firewall policy attached at the organization node with an explicit deny rule and no goto_next action
C) Firewall Insights recommendations enabled organization-wide
D) A default deny-egress VPC firewall rule

<details>
<summary>Answer</summary>

**Correct: B**

Hierarchical firewall policies attached at the organization or folder level are evaluated before VPC-level rules, and an explicit deny without goto_next cannot be overridden by lower-level project rules.

**Why the others are wrong:**
- Project-level VPC rules can be overridden or bypassed by other project-level rules and don't enforce org-wide policy
- Firewall Insights only provides recommendations, it does not enforce blocking behavior
- Deny-egress rules block outbound traffic, not inbound SSH from the internet

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the key architectural difference between a Terraform 'module' and a Terraform 'workspace'?

A) Modules manage remote state locking while workspaces manage provider versions
B) Modules only work with Deployment Manager templates
C) Workspaces store source code while modules store state files
D) A module is a reusable, parameterized collection of resources; a workspace is a named instance of state for the same configuration (e.g., dev/prod)

<details>
<summary>Answer</summary>

**Correct: D**

Modules encapsulate reusable resource definitions (like functions); workspaces let the same configuration maintain multiple independent state files, typically for environment separation.

**Why the others are wrong:**
- Neither construct directly manages locking or provider versions
- Modules are a Terraform-specific concept unrelated to Deployment Manager
- This reverses the actual roles — modules hold code, workspaces hold state instances, not the other way around

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---


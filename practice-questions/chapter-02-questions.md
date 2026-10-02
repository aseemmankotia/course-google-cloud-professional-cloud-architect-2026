## Chapter 2: Compute Selection & Migration Strategy — Practice Questions

**Q1.** EHR Healthcare needs to migrate 200 on-premises VMware VMs running legacy Windows and Linux appliances to Google Cloud with minimal application changes before a hard compliance deadline in 60 days. Which approach BEST meets this requirement?

A) Use Migrate to Virtual Machines to replicate the VMs to Compute Engine
B) Containerize each application and deploy to GKE Standard
C) Rewrite the applications as Cloud Functions
D) Export VM disks manually and re-create instances using Deployment Manager templates

<details>
<summary>Answer</summary>

**Correct: A**

Migrate to Virtual Machines performs agentless, automated replication of on-prem VMware/AWS/Azure VMs directly into Compute Engine with minimal downtime, matching the tight 60-day timeline and 'minimal changes' requirement — a textbook rehost (lift-and-shift).

**Why the others are wrong:**
- Containerizing to GKE is a re-architect effort that violates the 60-day/minimal-change constraint.
- Cloud Functions cannot run arbitrary legacy Windows/Linux appliances — wrong compute model entirely.
- Manual export/recreation is slow, error-prone, and doesn't scale to 200 VMs within the deadline.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Mountkirk Games' backend is a single monolithic binary that must scale to millions of concurrent players globally with low latency and independent scaling of matchmaking, leaderboard, and chat components. Which migration strategy should the architect recommend?

A) Lift-and-shift the monolith to a single large Compute Engine instance in one region
B) Re-platform the monolith onto App Engine Standard without code changes
C) Move the monolith into a single Cloud Function triggered by HTTP
D) Re-architect the monolith into microservices deployed on GKE across multiple regions

<details>
<summary>Answer</summary>

**Correct: D**

Independent scaling per component plus global low-latency multiplayer requirements demand decomposition into microservices with regional GKE clusters and global load balancing — a re-architect, not a rehost.

**Why the others are wrong:**
- A single large VM cannot independently scale components and creates a single point of failure globally.
- App Engine Standard has language/runtime restrictions and doesn't enable independent service scaling for a monolith without refactoring.
- Cloud Functions is stateless, event-driven, and unsuitable for a persistent, low-latency multiplayer monolith.

</details>

---

**Q3.** A team needs to run a stateless HTTP API that receives bursty traffic, must scale to zero when idle, and requires no Kubernetes management. Which compute service should they choose?

A) Cloud Run
B) GKE Autopilot
C) Compute Engine with a Managed Instance Group
D) App Engine Flexible

<details>
<summary>Answer</summary>

**Correct: A**

Cloud Run is purpose-built for stateless containers with request-based autoscaling, including scale-to-zero, and requires zero cluster management.

**Why the others are wrong:**
- GKE Autopilot still requires managing Kubernetes manifests/concepts and has a per-pod minimum footprint, adding unneeded complexity.
- MIGs scale on VM-level metrics with slower cold-start and don't natively scale to zero for request-driven APIs.
- App Engine Flexible has multi-minute VM startup times and does not scale to zero, failing the 'scale to zero when idle' requirement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company running a GKE Standard cluster wants to eliminate node-level patching, capacity planning, and per-node billing overhead for a variable containerized workload. What should they migrate to?

A) GKE Autopilot
B) Cloud Run for Anthos
C) A larger single-node GKE Standard cluster
D) Compute Engine sole-tenant nodes

<details>
<summary>Answer</summary>

**Correct: A**

GKE Autopilot removes node management entirely and bills per-pod resource requests, directly addressing node patching and capacity planning concerns while keeping the same Kubernetes API.

**Why the others are wrong:**
- Cloud Run for Anthos still runs on managed nodes the customer must maintain — it doesn't remove node management.
- A single larger node increases blast radius and doesn't remove patching/capacity planning responsibility.
- Sole-tenant nodes are for compliance/licensing isolation on Compute Engine, unrelated to container node management.

</details>

---

**Q5.** An architect configures a Managed Instance Group autoscaler with target CPU utilization of 60% and observes that new instances take longer than expected to receive traffic during a traffic spike. What is the MOST LIKELY cause?

A) The instance group has a maximum size of 1
B) Health checks are misconfigured to always fail
C) The autoscaler cooldown period is still counting the new instance's initial CPU spike toward the target
D) The region does not support autoscaling

<details>
<summary>Answer</summary>

**Correct: C**

The default MIG autoscaler cooldown period (60 seconds) intentionally excludes a new instance's initial startup CPU metrics from scaling decisions, which can appear as delayed responsiveness during rapid spikes — this is a well-known exam trap.

**Why the others are wrong:**
- A max size of 1 would prevent scaling entirely, not just delay it — the scenario states new instances ARE created.
- Failing health checks would keep instances out of the load balancer indefinitely, not just delay traffic — different symptom.
- Autoscaling is supported in all GCP regions; this is not a real limitation.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** EHR Healthcare must migrate an on-premises Microsoft SQL Server database with minimal downtime and continuous replication until cutover. Which GCP service should be used?

A) BigQuery Data Transfer Service
B) Database Migration Service
C) Cloud Storage Transfer Service
D) Datastream configured for BigQuery only

<details>
<summary>Answer</summary>

**Correct: B**

Database Migration Service supports continuous, minimal-downtime replication into Cloud SQL for SQL Server (and MySQL/PostgreSQL), matching the requirement exactly.

**Why the others are wrong:**
- BigQuery Data Transfer Service moves data into BigQuery for analytics, not operational database migration.
- Cloud Storage Transfer Service moves files/objects, not live relational database replication.
- Datastream is for change-data-capture streaming, primarily to BigQuery/Cloud Storage — not a full operational database migration path with cutover management.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which factor should drive the decision between Cloud Run and GKE Standard when selecting compute for a new containerized workload?

A) Whether fine-grained control over networking, node pools, and custom scheduling is required
B) Whether the workload uses Docker containers at all
C) Whether the workload runs in us-central1
D) Whether the workload is written in Go

<details>
<summary>Answer</summary>

**Correct: A**

The core decision axis in the compute selection tree is control vs. simplicity: GKE Standard gives full control over nodes, networking, and scheduling; Cloud Run trades that control for a fully managed, simpler experience.

**Why the others are wrong:**
- Both services run standard Docker/OCI containers — this isn't a differentiator.
- Region availability isn't the deciding architectural factor between these services.
- Programming language has no bearing on the Cloud Run vs. GKE decision since both are language-agnostic container platforms.

</details>

---

**Q8.** A batch job needs to process files uploaded to Cloud Storage, run for up to 45 minutes per invocation, and requires no server management. Which service is the correct fit?

A) App Engine Standard
B) Compute Engine with a startup script
C) Cloud Run job with a fixed 5-minute timeout
D) Cloud Functions (2nd gen) with a Cloud Storage trigger

<details>
<summary>Answer</summary>

**Correct: D**

Cloud Functions 2nd gen (built on Cloud Run) supports event-driven Cloud Storage triggers and timeouts long enough to cover a 45-minute run with no infrastructure to manage.

**Why the others are wrong:**
- App Engine Standard has strict request timeout limits and isn't event-driven from Cloud Storage in this way.
- Compute Engine requires managing the server lifecycle, violating the 'no server management' requirement.
- The option incorrectly states a fixed 5-minute Cloud Run timeout — Cloud Run timeouts are configurable up to 60 minutes, but as stated this option is capped incorrectly and would fail the 45-minute requirement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---


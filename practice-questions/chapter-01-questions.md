## Chapter 1: Cloud Architecture Design Fundamentals & The Four Case Studies — Practice Questions

**Q1.** TerramEarth's executives state: 'We currently learn about the health of a vehicle 3 months after a mechanical failure, when it is returned to a dealership. We would like to know what is happening with our vehicles in near real time.' Which architecture change BEST addresses this stated business requirement?

A) Build a streaming ingestion pipeline using Pub/Sub and Dataflow so vehicle telemetry is processed as it arrives
B) Increase the batch upload frequency from every 3 months to every 30 days
C) Add more storage capacity to the on-premises data center to hold vehicle logs longer
D) Require dealerships to manually enter vehicle diagnostic codes into a shared spreadsheet

<details>
<summary>Answer</summary>

**Correct: A**

The phrase 'near real time' is a non-functional requirement for low-latency, continuous data processing — Pub/Sub for ingestion plus Dataflow for streaming transformation is the canonical GCP pattern for IoT telemetry that must be analyzed as it arrives, not on a batch schedule.

**Why the others are wrong:**
- Shortening the batch interval is still batch processing — it does not satisfy 'near real time,' it only reduces staleness from months to weeks.
- More on-prem storage solves a capacity problem, not a latency/visibility problem — it doesn't get data to analysts faster.
- Manual entry is not scalable across 2 million vehicles and does not address the automation or real-time intent of the statement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Helicopter Racing League (HRL) wants spectators on every continent to experience minimal delay when watching live races, and wants to reduce load on origin video encoding servers during peak events. Which combination of services BEST meets these requirements?

A) A single regional Compute Engine instance running a custom video server, scaled vertically
B) Cloud SQL replicas in each viewer region to cache video segments
C) A single global HTTP(S) load balancer with no caching layer, relying on backend autoscaling alone
D) Cloud CDN in front of the video streaming backend, with encoding jobs distributed across multiple regions

<details>
<summary>Answer</summary>

**Correct: D**

Global low-latency video delivery at scale requires edge caching (Cloud CDN) to serve viewers from the nearest point of presence, combined with distributed/multi-region encoding to avoid a single origin bottleneck — this is the standard HRL exam-tested pattern for live global media.

**Why the others are wrong:**
- Vertical scaling of a single regional instance cannot serve global low-latency traffic and is a single point of failure.
- Cloud SQL is a relational database, not a media caching or delivery mechanism — it cannot cache video segments.
- A global load balancer without a CDN still routes every request back to origin, failing to reduce latency or origin load.

</details>

---

**Q3.** EHR Healthcare must maintain connectivity between its on-premises data centers, its GCP environment, and an existing AWS environment, while meeting strict encryption and compliance requirements for patient data. Which architecture decision BEST satisfies the hybrid/multi-cloud and compliance requirements together?

A) Migrate all AWS workloads to GCP immediately to eliminate the multi-cloud requirement
B) Use public internet connectivity with application-level TLS only, since it is encrypted in transit
C) Establish HA VPN or Dedicated Interconnect between on-prem and GCP, use a supported cross-cloud connectivity path to AWS, and enforce encryption at rest and in transit across all environments
D) Store all patient data only in the on-premises data center and use GCP solely for stateless compute

<details>
<summary>Answer</summary>

**Correct: C**

EHR's requirements explicitly include maintaining hybrid connectivity (on-prem + GCP + AWS) and encrypting data at rest and in transit — HA VPN/Interconnect for reliable private connectivity plus enforced encryption everywhere satisfies both the compliance and hybrid-architecture constraints simultaneously.

**Why the others are wrong:**
- Immediate full migration off AWS contradicts the case study's explicit hybrid/multi-cloud requirement and is not a stated business goal.
- Public internet with only application-level TLS does not meet enterprise compliance expectations for private connectivity and ignores encryption-at-rest requirements.
- Keeping all patient data on-prem while using GCP only for stateless compute ignores the requirement to reduce on-prem footprint and improve scalability/reliability via cloud migration.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Mountkirk Games is launching a new mobile multiplayer game expected to have millions of concurrent players worldwide, with a requirement for low-latency matchmaking and zero-downtime deployments. Which GCP approach BEST fits these requirements?

A) A single zonal GKE cluster in one region, scaled up as demand grows
B) A single Compute Engine VM per game region, manually resized during peak hours
C) App Engine standard environment only, with no container orchestration
D) Multiple regional GKE clusters distributed near player populations, behind a global load balancer, with rolling deployments

<details>
<summary>Answer</summary>

**Correct: D**

Global low-latency multiplayer at massive scale requires regional GKE clusters placed close to players, fronted by a global load balancer for routing, with rolling/zero-downtime deployments — this matches Mountkirk's explicit technical requirements for latency and no-downtime releases.

**Why the others are wrong:**
- A single zonal cluster cannot provide global low latency and is a single point of failure for a worldwide launch.
- Manually resized single VMs per region cannot handle dynamic scaling or provide zero-downtime deployment guarantees.
- App Engine standard alone doesn't give the container orchestration and custom game-server session management Mountkirk's real-time multiplayer backend needs.

</details>

---

**Q5.** Which GCP service is the correct choice for ingesting high-volume, high-frequency telemetry data from 2 million connected vehicles, each generating 120-200 data points per second, before it is processed by a streaming pipeline?

A) Pub/Sub
B) Cloud Tasks
C) Cloud Scheduler
D) Firestore

<details>
<summary>Answer</summary>

**Correct: A**

Pub/Sub is GCP's managed, globally scalable messaging service designed for exactly this pattern: massive-scale, high-throughput event ingestion decoupled from downstream processing (e.g., Dataflow), which fits TerramEarth's IoT telemetry volume.

**Why the others are wrong:**
- Cloud Tasks is designed for reliable execution of discrete application tasks/queues, not high-volume telemetry stream ingestion.
- Cloud Scheduler triggers jobs on a cron-like schedule; it is not an ingestion mechanism for continuous sensor data.
- Firestore is a document database for application state, not designed as a high-throughput ingestion buffer for millions of events per second.

</details>

---

**Q6.** A design review for EHR Healthcare specifies that connectivity between the on-premises data center and GCP must have no single point of failure and must maintain a 99.99% availability SLA. Which VPN configuration satisfies this requirement?

A) A single Classic VPN tunnel to one Cloud VPN gateway
B) HA VPN with two tunnels to two interfaces of an HA VPN gateway, using two on-premises peer devices/tunnels
C) A single HA VPN tunnel to one Cloud VPN gateway interface
D) Classic VPN with static routing and a single peer IP

<details>
<summary>Answer</summary>

**Correct: B**

Google Cloud's documented HA VPN configuration that qualifies for the 99.99% SLA requires two tunnels from two interfaces of an HA VPN gateway connected to two separate peer VPN gateways/tunnels — eliminating single points of failure on both sides.

**Why the others are wrong:**
- A single Classic VPN tunnel has no redundancy and does not meet an HA SLA target.
- A single HA VPN tunnel, even using the HA gateway type, does not achieve the 99.99% SLA — the redundant two-tunnel topology is required.
- Classic VPN with static routing and a single peer IP has no failover path and does not meet the availability requirement.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** HRL's disaster recovery requirement states that live race broadcasting must resume within 1 minute of a regional outage, with no more than 5 seconds of data loss. What do these two numbers represent in architecture planning?

A) RPO of 1 minute and RTO of 5 seconds
B) SLA of 1 minute and SLO of 5 seconds
C) RTO of 1 minute and RPO of 5 seconds
D) Both numbers represent the same metric, expressed differently

<details>
<summary>Answer</summary>

**Correct: C**

Recovery Time Objective (RTO) is how long it takes to resume service after an outage (1 minute); Recovery Point Objective (RPO) is the maximum acceptable data loss measured in time (5 seconds) — the exam frequently tests correctly mapping business statements to these two distinct metrics.

**Why the others are wrong:**
- This reverses the definitions — resuming service is RTO, not RPO, and data loss tolerance is RPO, not RTO.
- SLA/SLO describe service commitments and measurable targets in general, not the specific recovery-time and data-loss metrics being described here.
- RTO and RPO are distinct metrics measuring different things (time-to-recover vs. acceptable data loss) — they are never interchangeable.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** In the Professional Cloud Architect trade-off framework, an executive says 'We need the absolute lowest cost possible' while a technical requirement elsewhere in the same case study demands 99.99% availability across multiple regions. What is the correct way to resolve this conflict in an architecture proposal?

A) Design for the stated availability target and clearly document the cost trade-off, since HA requirements are typically non-negotiable constraints while cost statements represent optimization goals within those constraints
B) Always prioritize the cost statement because it comes from an executive
C) Always prioritize the availability requirement because it is stated in a technical requirements list
D) Ignore both and choose the cheapest single-region single-zone design to simplify the architecture

<details>
<summary>Answer</summary>

**Correct: A**

PCA exam scenarios consistently treat explicit non-functional requirements (like a stated availability SLA) as hard constraints, while broad cost statements are optimization goals to pursue within those constraints — the correct answer designs to meet the HA target while optimizing cost elsewhere (e.g., committed use discounts, autoscaling) and explicitly documents the trade-off.

**Why the others are wrong:**
- Blindly prioritizing any statement based only on who said it (executive vs. engineer) ignores the actual technical constraints of the system.
- While availability requirements are usually hard constraints, the correct answer isn't to ignore cost entirely — it's to satisfy HA and still optimize cost, which this option fails to state.
- A single-zone design would violate the explicit 99.99% availability requirement and is never correct when HA is explicitly specified.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---


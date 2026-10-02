## Chapter 3: Networking, Multi-Region HA & Disaster Recovery Design — Practice Questions

**Q1.** HRL streams live video globally and needs the lowest possible latency for viewers on every continent, with encoding clusters running in multiple regions and automatic failover if a region goes down. Which architecture BEST meets these requirements?

A) Deploy a Regional external Application Load Balancer in each region and use separate DNS A records with manual geo-based routing
B) Deploy a single Network Load Balancer (passthrough) in the region closest to HQ and rely on client-side retries
C) Deploy an Internal Application Load Balancer in each region and connect them with VPC Peering
D) Deploy a Global external Application Load Balancer with Cloud CDN in front of multi-region backend services, using a single anycast IP

<details>
<summary>Answer</summary>

**Correct: D**

A Global external Application Load Balancer publishes one anycast IP; Google's edge network routes each viewer to the nearest healthy backend, and Cloud CDN caches segments at the edge — exactly the low-latency, HA, multi-region pattern the exam expects for global streaming.

**Why the others are wrong:**
- Regional LBs with manual DNS round-robin have no health-aware routing and add DNS TTL latency on failover
- A single-region Network LB has no multi-region presence and is a single point of failure
- Internal LBs are not internet-facing and VPC Peering does not provide global traffic distribution

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company has 10 application teams, each in its own GCP project. A central network security team must enforce consistent firewall rules and subnet allocation across all teams, and all projects must reach the same on-prem network through one hybrid connection. Which design BEST satisfies this?

A) Create VPC Peering connections between all 10 project VPCs in a full mesh
B) Give each team its own VPC and connect them to on-prem with 10 separate Cloud VPN tunnels
C) Configure a Shared VPC with the network team owning the host project and each team attached as a service project
D) Merge all 10 teams into a single GCP project with one VPC

<details>
<summary>Answer</summary>

**Correct: C**

Shared VPC lets a central host project own subnets, firewall rules, and hybrid connectivity, while service projects consume those subnets — giving centralized administration exactly as required, without merging billing or IAM boundaries.

**Why the others are wrong:**
- VPC Peering is non-transitive and does not centralize firewall/subnet administration; a 10-way mesh is also an operational nightmare
- 10 separate VPN tunnels duplicates hybrid connectivity and firewall management with no central control
- A single project removes the project-level billing/IAM isolation the teams need

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company has a steady 8 Gbps of traffic between its on-prem data center and GCP, needs traffic to avoid the public internet, and has equipment already colocated in a facility that offers direct access to Google's network. Which connectivity option BEST fits?

A) Cloud VPN (HA VPN) over the public internet
B) Partner Interconnect
C) Direct Peering with Google
D) Dedicated Interconnect

<details>
<summary>Answer</summary>

**Correct: D**

Dedicated Interconnect provides a direct 10 Gbps or 100 Gbps circuit at a Google colocation facility, avoiding the internet entirely — the right fit when the customer already has equipment in a supported colocation facility and needs steady high bandwidth.

**Why the others are wrong:**
- HA VPN encrypts traffic over the public internet and has lower/variable throughput and latency than a direct circuit
- Partner Interconnect is used when the customer is NOT in a Google colocation facility and needs a partner to extend the connection
- Direct Peering connects to Google's edge network for Google services/public IPs, not for private access into a customer VPC for hybrid workloads

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which GCP load balancer type provides a single global anycast IP address and routes HTTP(S) requests to the closest healthy backend across multiple regions?

A) Regional external Application Load Balancer
B) Internal Application Load Balancer
C) Global external Application Load Balancer
D) Internal TCP/UDP Load Balancer

<details>
<summary>Answer</summary>

**Correct: C**

The Global external Application Load Balancer (formerly Global HTTP(S) Load Balancing) uses a single anycast VIP and Google's global network to send users to the nearest healthy regional backend.

**Why the others are wrong:**
- Regional external Application LB serves one region only, with no global anycast routing
- Internal Application LB is L7 but scoped to internal clients within a region/VPC, not internet-facing
- Internal TCP/UDP LB is a regional Layer 4 passthrough LB with no HTTP(S) routing or global reach

</details>

---

**Q5.** A set of internal microservices in a single region need Layer 7 path-based routing and HTTP health checks, but must never be reachable from the public internet. Which load balancer should be used?

A) Regional internal Application Load Balancer
B) Global external Application Load Balancer
C) External passthrough Network Load Balancer
D) Internal passthrough TCP/UDP Load Balancer

<details>
<summary>Answer</summary>

**Correct: A**

The Regional internal Application Load Balancer is L7, supports path/host-based routing and HTTP(S) health checks, and its VIP is only reachable from within the VPC — matching all stated requirements.

**Why the others are wrong:**
- Global external Application LB is internet-facing, violating the 'never public' requirement
- External passthrough Network LB is internet-facing and Layer 4 only
- Internal passthrough TCP/UDP LB is internal but Layer 4 — it cannot do path-based HTTP routing

</details>

---

**Q6.** VMs in a subnet have only internal IP addresses but must call Cloud Storage and BigQuery APIs directly. What is the minimum required configuration to allow this?

A) Assign external IP addresses to the VMs
B) Create a VPC Peering connection to a Google-managed API project
C) Enable Private Google Access on the subnet
D) Deploy Cloud NAT and disable Private Google Access

<details>
<summary>Answer</summary>

**Correct: C**

Private Google Access lets VMs with only internal IPs reach Google APIs and services (e.g., Cloud Storage, BigQuery) over Google's internal network path, without needing an external IP.

**Why the others are wrong:**
- Assigning external IPs works but violates the internal-only requirement and is not minimal/best practice
- There is no such thing as VPC Peering to a Google-managed API project
- Cloud NAT can also enable outbound API access but is unnecessary overhead when Private Google Access is designed exactly for this case; disabling Private Google Access is backwards

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** To achieve the 99.99% availability SLA with Cloud HA VPN, what is the minimum required configuration on the GCP side?

A) An HA VPN gateway with two interfaces, each connected via a tunnel to two separate interfaces on a redundant peer VPN gateway
B) A single VPN tunnel using static routing to the on-prem gateway
C) Classic VPN with two tunnels to the same peer gateway interface
D) A single HA VPN interface with two tunnels to one peer IP address

<details>
<summary>Answer</summary>

**Correct: A**

HA VPN's 99.99% SLA requires both of its two interfaces to be used, each connected to a separate interface on a redundant peer gateway, so there is no single point of failure on either side.

**Why the others are wrong:**
- A single tunnel has no redundancy and only qualifies for a lower SLA
- Classic VPN is being deprecated for new deployments and only offers a 99.9% SLA even with two tunnels
- Using only one HA VPN interface, even with two tunnels, does not meet the redundant-interface requirement for 99.99%

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What does 'non-transitive' mean in the context of VPC Peering?

A) Peered VPCs cannot use IPv6 addressing
B) Peering connections automatically expire after 24 hours and must be renewed
C) Peered VPCs must be created in the same GCP region
D) If VPC A peers with VPC B, and VPC B peers with VPC C, VPC A cannot reach VPC C through VPC B

<details>
<summary>Answer</summary>

**Correct: D**

Non-transitivity is the core limitation of VPC Peering: connectivity is strictly point-to-point between the two directly peered networks and is never extended through an intermediary peered network.

**Why the others are wrong:**
- Non-transitivity has nothing to do with IP version support
- Peering connections do not expire on a timer
- VPC Peering is global by design and does not require matching regions

</details>

---


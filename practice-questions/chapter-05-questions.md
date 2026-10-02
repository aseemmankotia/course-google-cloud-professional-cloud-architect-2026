## Chapter 5: Storage & Data Solutions Provisioning — Practice Questions

**Q1.** A logistics company ingests location pings from 2 million delivery vehicles every second. Data is written once, read mostly by row-key range for recent time-series analysis, and the schema needs to scale horizontally without manual resharding. Which service should you provision?

A) Cloud Bigtable
B) Cloud SQL for PostgreSQL with read replicas
C) Cloud Spanner
D) Firestore in Native mode

<details>
<summary>Answer</summary>

**Correct: A**

Bigtable is purpose-built for high-throughput, low-latency time-series/IoT workloads with row-key based access and linear horizontal scaling by adding nodes.

**Why the others are wrong:**
- Cloud SQL is regional and vertically limited (max 64TB storage); it cannot sustain millions of writes/sec.
- Spanner is optimized for strongly-consistent relational transactions, not raw high-throughput time-series ingestion — it costs far more for this pattern.
- Firestore is a document database tuned for app/mobile sync workloads, not massive time-series telemetry throughput.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A global bank needs a relational database with external strong consistency, SQL semantics, ACID transactions across regions, and 99.999% availability. Which service meets these requirements?

A) Cloud SQL with cross-region read replicas
B) Cloud Spanner multi-region configuration
C) Cloud Bigtable with multi-cluster routing
D) BigQuery with multi-region datasets

<details>
<summary>Answer</summary>

**Correct: B**

Spanner multi-region configurations provide 99.999% SLA, external consistency, and horizontally scalable SQL/ACID transactions across regions via TrueTime and Paxos.

**Why the others are wrong:**
- Cloud SQL read replicas are asynchronous and eventually consistent — no cross-region strong consistency or that SLA tier.
- Bigtable is NoSQL wide-column, not relational, and has no ACID multi-row transactions across regions.
- BigQuery is an analytical warehouse, not designed for OLTP transactional consistency.

</details>

---

**Q3.** Your company must retain compliance audit videos for 7 years. The videos are accessed less than once per year, only during audits. Which storage class should you assign at object creation to minimize cost?

A) Standard, with a lifecycle rule to transition to Nearline after 30 days
B) Nearline, with a lifecycle rule to transition to Coldline after 90 days
C) Archive storage class from creation
D) Coldline, with a lifecycle rule to transition to Archive after 365 days

<details>
<summary>Answer</summary>

**Correct: C**

Access frequency of less than once per year maps directly to Archive tier, the cheapest class, and the 7-year retention easily exceeds the 365-day minimum storage duration, avoiding early-deletion fees.

**Why the others are wrong:**
- Standard is the most expensive tier and unnecessary for yearly access — pure waste of budget.
- Nearline targets monthly access patterns, not yearly, and costs more than Archive long-term.
- Staging through Coldline first adds complexity and cost with no benefit since access pattern is already known upfront.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A marketing team needs ad-hoc SQL queries over 3 petabytes of clickstream data and wants a real-time dashboard refreshed every few minutes, without managing any servers. Which service should you provision?

A) Cloud Spanner with a read-heavy instance configuration
B) Cloud Bigtable with a large HDD cluster
C) Cloud SQL for MySQL with high memory tier
D) BigQuery

<details>
<summary>Answer</summary>

**Correct: D**

BigQuery is the serverless, petabyte-scale analytics warehouse designed for ad-hoc SQL and near-real-time dashboards via streaming inserts.

**Why the others are wrong:**
- Spanner is not designed or priced for petabyte-scale analytical scans; it's OLTP-oriented.
- Bigtable lacks native SQL and is not intended for ad-hoc analytical queries across a dashboard tool.
- Cloud SQL cannot scale to petabytes and is not serverless at that scale.

</details>

---

**Q5.** Vehicle telemetry must be processed so that messages from the same vehicle are delivered to subscribers in the exact order they were published, while messages from different vehicles can still be processed in parallel. Which Pub/Sub configuration achieves this?

A) Enable exactly-once delivery on the subscription
B) Create a FIFO-type topic and attach a single subscriber
C) Enable message ordering and set the ordering key to the vehicle ID
D) Increase the acknowledgement deadline to 600 seconds

<details>
<summary>Answer</summary>

**Correct: C**

Pub/Sub supports ordered delivery per ordering key; setting ordering key to vehicle ID guarantees per-vehicle order while allowing parallel processing across different keys.

**Why the others are wrong:**
- Exactly-once delivery controls duplicate suppression, not ordering.
- Pub/Sub does not have a 'FIFO topic type' — that is an AWS SQS concept, a classic exam trap.
- Ack deadline affects redelivery timing on failure, not message order.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A Dataflow streaming pipeline must compute 5-minute rolling counts of vehicle telemetry events while tolerating events that arrive up to 2 minutes late due to mobile network delays. Which windowing configuration should you use?

A) Global window with a repeating default trigger
B) Session windows with a 5-minute gap duration
C) Sliding windows with a 1-minute period and no lateness handling
D) Fixed windows of 5 minutes with allowed lateness of 2 minutes

<details>
<summary>Answer</summary>

**Correct: D**

Fixed windows of 5 minutes match the required aggregation interval, and setting allowed lateness lets the pipeline accept and incorporate late-arriving data before the window closes permanently.

**Why the others are wrong:**
- Global windows require custom triggers and don't naturally express fixed 5-minute periodic aggregation.
- Session windows group by activity gaps, not fixed time intervals — wrong pattern for rolling counts.
- Sliding windows without lateness handling would drop the late 2-minute events entirely.

</details>

---

**Q7.** What is the key architectural difference between a Cloud SQL High Availability configuration and a Cloud Spanner multi-region configuration?

A) Cloud SQL HA replicates asynchronously across multiple regions, while Spanner only supports a single zone
B) Cloud SQL HA synchronously replicates to a standby in a different zone of the same region for failover, while Spanner synchronously replicates across regions using a Paxos-based consensus, enabling horizontal write scaling
C) Both services use an identical replication model; only their pricing tiers differ
D) Cloud SQL automatically shards data across nodes exactly like Spanner

<details>
<summary>Answer</summary>

**Correct: B**

Cloud SQL HA is a regional failover pattern (primary + standby in different zones), while Spanner uses distributed consensus replication across regions/zones that also enables horizontal scale-out for writes — a fundamentally different architecture.

**Why the others are wrong:**
- Cloud SQL HA replication is synchronous within-region, not asynchronous cross-region.
- Pricing is not the differentiator; the underlying replication and scaling architecture is.
- Cloud SQL does not auto-shard; it scales vertically up to its max instance size, unlike Spanner's horizontal sharding.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A mobile application needs a NoSQL document database that supports real-time client synchronization, offline data access, and automatic multi-region replication for user profile data. Which service should you choose?

A) Cloud Bigtable
B) Firestore
C) Cloud Spanner
D) BigQuery with streaming inserts

<details>
<summary>Answer</summary>

**Correct: B**

Firestore is the document database explicitly designed for mobile/web apps, offering real-time listeners, offline persistence SDKs, and multi-region replication out of the box.

**Why the others are wrong:**
- Bigtable has no native mobile SDKs, offline sync, or real-time listener support.
- Spanner is relational/SQL and not designed for client-side real-time sync or offline caching.
- BigQuery is an analytics warehouse, unsuitable for low-latency transactional mobile app reads/writes.

</details>

---


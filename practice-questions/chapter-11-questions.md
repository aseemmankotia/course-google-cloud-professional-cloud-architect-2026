## Chapter 11: SRE Practices, Observability & Disaster Recovery — Practice Questions

**Q1.** Your service has an SLO of 99.95% availability measured over a rolling 30-day window. How many minutes of downtime does the error budget allow?

A) 4.32 minutes
B) 43.2 minutes
C) 216 minutes
D) 21.6 minutes

<details>
<summary>Answer</summary>

**Correct: D**

30 days = 43,200 minutes. Error budget = 100% - 99.95% = 0.05%. 0.05% of 43,200 = 21.6 minutes.

**Why the others are wrong:**
- 4.32 minutes is the budget for a 99.99% SLO, not 99.95%.
- 43.2 minutes is the budget for a 99.9% SLO.
- 216 minutes would correspond to a 99.5% SLO.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team notices intermittent high latency in a microservices application running on GKE and needs to identify which downstream service call is contributing the most delay. Which tool should they use first?

A) Error Reporting
B) Cloud Logging
C) Cloud Trace
D) Cloud Profiler

<details>
<summary>Answer</summary>

**Correct: C**

Cloud Trace captures per-request latency across service calls and displays a waterfall of spans, pinpointing which hop adds delay.

**Why the others are wrong:**
- Error Reporting groups exceptions/stack traces, not latency data.
- Cloud Logging shows log entries but doesn't correlate distributed latency by default.
- Cloud Profiler analyzes CPU/memory consumption inside a single process, not cross-service latency.

</details>

---

**Q3.** You need to alert when a Cloud Run service returns more than 50 HTTP 500 errors within a 5-minute window. What is the correct configuration?

A) Create a log-based counter metric filtered on severity=ERROR and status_code=500, then create an alerting policy with a threshold of 50 over a 5-minute window
B) Create an uptime check with content matching and alert on check failure
C) Enable Error Reporting and configure a daily digest email
D) Create a distribution log-based metric and alert on p99 latency

<details>
<summary>Answer</summary>

**Correct: A**

A counter log-based metric counts matching log entries; an alerting policy with a rolling 5-minute window and threshold of 50 triggers exactly on this condition.

**Why the others are wrong:**
- Uptime checks test endpoint reachability, not error-count thresholds inside logs.
- Error Reporting digests are daily summaries, not near-real-time threshold alerts.
- A distribution metric measures numeric value distributions like latency, not discrete error counts.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company is migrating a stateful legacy application and requires the ability to switch all traffic to a new version instantly and roll back immediately if issues occur. They have budget to run duplicate environments temporarily. Which deployment strategy BEST fits?

A) Rolling update
B) Blue-green deployment
C) Canary release
D) Shadow deployment

<details>
<summary>Answer</summary>

**Correct: B**

Blue-green deployment runs two full environments and switches traffic instantly via router/load balancer change, enabling immediate rollback by reverting the switch.

**Why the others are wrong:**
- Rolling updates replace instances incrementally, so there is no instant full cutover or immediate full rollback.
- Canary releases gradually shift a small traffic percentage; it is not an instant full cutover.
- Shadow deployment mirrors traffic for testing without serving real users, so it doesn't serve as a release/rollback mechanism.

</details>

---

**Q5.** Your finance application requires an RTO of under 5 minutes and an RPO near zero. Cost is not the primary constraint. Which disaster recovery pattern should you implement?

A) Backup and restore
B) Multi-region active-active
C) Pilot light
D) Warm standby

<details>
<summary>Answer</summary>

**Correct: B**

Multi-region active-active serves live traffic from multiple regions simultaneously with continuous data replication, achieving near-zero RTO and RPO.

**Why the others are wrong:**
- Backup and restore has the highest RTO/RPO of all patterns, unsuitable for these tight requirements.
- Pilot light keeps only core components running, requiring scale-up time that exceeds 5 minutes for most workloads.
- Warm standby reduces RTO further than pilot light but still requires scale-up and typically cannot guarantee near-zero RPO for all data.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Which statement correctly differentiates an SLI from an SLO?

A) SLI is a quantitative measurement of service behavior; SLO is a target value or range for that measurement
B) SLI is a contractual promise to customers; SLO is the internal target
C) SLO is measured in real time; SLI is a business agreement
D) There is no difference; the terms are used interchangeably

<details>
<summary>Answer</summary>

**Correct: A**

SLI (Service Level Indicator) is the measured metric, e.g., request latency or availability percentage. SLO (Service Level Objective) is the target/threshold set for that SLI.

**Why the others are wrong:**
- The contractual promise with penalties describes an SLA, not an SLI.
- SLO is a target, not a real-time measurement; SLI is the measurement, not a business agreement.
- SLI, SLO, and SLA are distinct terms tested separately on the exam.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Your organization needs Admin Activity audit logs retained for compliance purposes. What is the default retention period for the _Required log bucket in Cloud Logging, and can it be changed?

A) 30 days, configurable up to 3650 days
B) 90 days, configurable up to 400 days
C) 400 days, configurable up to 3650 days
D) 400 days, not configurable

<details>
<summary>Answer</summary>

**Correct: D**

The _Required bucket holds Admin Activity, System Event, Access Transparency, and Policy Denied audit logs with a fixed 400-day retention that cannot be modified.

**Why the others are wrong:**
- 30 days configurable up to 3650 describes the _Default bucket and user-defined buckets, not _Required.
- 90 days is not a Cloud Logging retention default for any standard bucket.
- The 400-day retention for _Required logs is fixed and cannot be extended to 3650 days.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A team needs full observability for a Cloud Run service including metrics dashboards, centralized logs, distributed tracing, and automatic error grouping. Which single combination of Google Cloud operations tools together satisfies all four requirements?

A) Cloud Monitoring + Cloud Profiler only
B) Cloud Logging + Cloud Asset Inventory + Cloud Trace
C) Cloud Monitoring + Cloud Logging + Cloud Trace + Error Reporting
D) Cloud Monitoring + Cloud Logging only

<details>
<summary>Answer</summary>

**Correct: C**

Cloud Monitoring provides dashboards/alerting, Cloud Logging centralizes logs, Cloud Trace provides distributed latency tracing, and Error Reporting automatically groups and surfaces errors — together covering all four stated needs.

**Why the others are wrong:**
- Cloud Profiler analyzes code-level CPU/memory performance, not tracing or error grouping.
- Cloud Asset Inventory tracks resource inventory/configuration, not logs, metrics, or tracing.
- Omitting Cloud Trace and Error Reporting leaves distributed tracing and automatic error grouping unmet.

</details>

---


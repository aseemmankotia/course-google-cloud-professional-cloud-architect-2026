## Chapter 9: Business Process, Stakeholder Management & Cost Optimization — Practice Questions

**Q1.** A retail company's data science team has no computer vision expertise and needs to launch a product-photo tagging feature in 6 weeks for a holiday launch. Which approach BEST satisfies the build-vs-buy constraint?

A) Hire ML engineers and train a custom TensorFlow model on GKE
B) Build a custom CNN using Vertex AI Training with a 3-month timeline
C) Use the Vision API for label detection and integrate via REST calls
D) Outsource model development to a third-party consultancy on a 4-month contract

<details>
<summary>Answer</summary>

**Correct: C**

Vision API is a fully managed pre-trained service requiring no ML expertise, integrates in days, and meets the 6-week time-to-market constraint without a skill investment.

**Why the others are wrong:**
- Custom model training requires ML expertise the team lacks and cannot realistically finish in 6 weeks
- Vertex AI custom training still requires ML skills and a longer timeline than the deadline allows
- External consultancy contract exceeds the 6-week deadline and adds vendor management overhead

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An executive tells the board the company will reduce cloud spend by 30% next quarter while keeping full flexibility to change instance shapes weekly for an unpredictable workload. Which cost optimization approach reconciles this statement with the technical roadmap?

A) 1-year resource-based committed use discount on fixed machine types
B) 3-year resource-based committed use discount on fixed machine types
C) Sustained use discounts combined with rightsizing recommendations
D) Reserved capacity purchased through a third-party reseller

<details>
<summary>Answer</summary>

**Correct: C**

Sustained use discounts apply automatically without commitment and rightsizing recommendations continuously adjust machine types, preserving flexibility while still lowering cost — matching the executive's dual promise.

**Why the others are wrong:**
- Resource-based CUDs lock in a specific machine type/family, breaking the weekly flexibility requirement
- A 3-year CUD is even less flexible and riskier for an unpredictable workload
- Third-party reseller reserved capacity still locks configuration and doesn't address unpredictability

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A bank operating under strict regulatory audit requirements wants to migrate a core ledger system to GCP but requires every production change to be reviewed and approved before rollout. Which change management practice BEST fits this risk-averse environment?

A) Continuous deployment directly to production with automated rollback
B) A staged rollout pipeline with mandatory manual approval gates and audit logging at each stage
C) Feature flags enabled in production with no formal review process
D) Blue-green deployment with automatic promotion after a 5-minute canary

<details>
<summary>Answer</summary>

**Correct: B**

Regulated organizations require documented, auditable approval gates before each production change; a staged pipeline with manual sign-off and logging satisfies compliance and change control needs.

**Why the others are wrong:**
- Continuous deployment bypasses required manual review, unacceptable for regulated change control
- Feature flags without review provide no audit trail or approval gate
- Automatic promotion after a short canary removes the human approval step regulators require

</details>

---

**Q4.** A company runs a stable fleet of 200 N2 VMs with predictable usage for the next 3 years and no plans to change machine family. Which discount option maximizes savings?

A) 3-year resource-based committed use discount
B) 1-year flexible (spend-based) committed use discount
C) Sustained use discounts only
D) 3-year flexible (spend-based) committed use discount

<details>
<summary>Answer</summary>

**Correct: A**

For a stable, unchanging fixed machine type over 3 years, a resource-based CUD gives the highest discount (up to ~55% for most machine families) since it targets a specific vCPU/memory commitment.

**Why the others are wrong:**
- 1-year flexible CUD gives a lower discount rate and isn't optimal when the resource shape won't change
- Sustained use discounts (max 30%, N1-only) provide less savings than a matched 3-year commitment
- Flexible CUDs trade some discount for cross-service flexibility, which isn't needed here since the fleet is fixed

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A company spends money across Compute Engine, GKE Autopilot, and Cloud Run, and the mix of services shifts month to month based on project needs. Which commitment type is BEST suited to capture savings across this varying portfolio?

A) Resource-based committed use discount
B) Sustained use discount
C) Committed use discount for VMware Engine only
D) Flexible (spend-based) committed use discount

<details>
<summary>Answer</summary>

**Correct: D**

Flexible CUDs commit to an hourly spend amount and automatically apply across eligible services (Compute Engine, GKE, Cloud Run, Cloud Functions), making them ideal when the underlying service mix changes.

**Why the others are wrong:**
- Resource-based CUDs are tied to a specific machine type/region and don't transfer across service types
- Sustained use discounts only apply to N1 machine types on Compute Engine, not GKE/Cloud Run
- VMware Engine CUDs are scoped only to VMware Engine nodes, not the described mixed portfolio

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Which GCP capability should an architect use to generate ongoing machine-type rightsizing suggestions based on historical CPU and memory utilization?

A) Cloud Monitoring uptime checks
B) Cloud Billing budget alerts
C) Recommender API (VM machine type recommender)
D) Cloud Asset Inventory

<details>
<summary>Answer</summary>

**Correct: C**

The Recommender API's machine type recommender analyzes 8/14/30-day utilization history and suggests rightsizing (upsize/downsize) to reduce waste.

**Why the others are wrong:**
- Uptime checks only test availability, not resource utilization for rightsizing
- Budget alerts notify on spend thresholds but don't recommend machine type changes
- Asset Inventory tracks resource metadata, not utilization-based sizing recommendations

</details>

---

**Q7.** When building a total cost of ownership (TCO) model to justify a cloud migration to executives, which factor is MOST often omitted but required for an accurate comparison?

A) On-premises hardware purchase cost
B) Cloud compute instance hourly pricing
C) Cloud storage per-GB pricing
D) Staff retraining, migration labor, and ongoing operational overhead

<details>
<summary>Answer</summary>

**Correct: D**

TCO models frequently capture direct infrastructure costs but omit indirect costs like staff retraining, migration effort, and operational overhead, which materially affect the business case.

**Why the others are wrong:**
- Hardware purchase cost is a standard, commonly included on-prem baseline figure
- Compute hourly pricing is a standard, easily obtained cloud cost input
- Storage pricing is a standard, easily obtained cloud cost input

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Product management is pressuring the team to ship three new features next sprint, while the architecture team has flagged a growing backlog of technical debt in the data pipeline that is starting to cause intermittent failures. What is the BEST way to align these competing priorities?

A) Ignore technical debt until a major outage forces a fix
B) Halt all feature work for a full quarter to address technical debt
C) Present the failure risk and business impact to stakeholders and negotiate a fixed percentage of sprint capacity dedicated to debt reduction
D) Let engineers silently allocate time to debt reduction without informing stakeholders

<details>
<summary>Answer</summary>

**Correct: C**

Effective stakeholder management requires making the risk/impact visible and negotiating a transparent, sustainable capacity split (e.g., 20% of sprint) rather than an all-or-nothing approach.

**Why the others are wrong:**
- Ignoring debt increases risk of outages and violates responsible technical stewardship
- A full quarter halt is an extreme, rarely justified response that damages stakeholder trust and feature delivery
- Silently reallocating time without stakeholder visibility undermines trust and transparency in the process

</details>

---


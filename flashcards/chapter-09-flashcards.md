## Chapter 9: Business Process, Stakeholder Management & Cost Optimization — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Resource-based CUD (Compute Engine) discount for 1-year vs 3-year commitment? | ~37% (1-year) vs ~55% (3-year) off on-demand price. Locked to specific machine type/family/region. Exam tip: use when workload shape is stable and won't change. |
| 2 | Sustained Use Discount (SUD) — what machine types and max discount? | Applies automatically to N1 predefined/custom machine types only; up to 30% discount for running a full billing month. No commitment required, no upfront purchase. |
| 3 | Flexible (spend-based) CUD — what does it cover? | A committed hourly spend amount (1yr or 3yr) that automatically applies across Compute Engine, GKE, Cloud Run, Cloud Functions, and VMware Engine. Best for mixed/varying service portfolios. |
| 4 | Resource-based CUD vs Flexible CUD — when to choose which? | Resource-based: fixed machine type/family for 1-3yrs, higher discount. Flexible: spend commitment across multiple compute services, lower discount but more flexibility. Exam tip: match discount vehicle to workload stability. |
| 5 | Which GCP tool generates VM rightsizing recommendations? | Recommender API (machine type recommender) — analyzes 8/14/30-day CPU/memory utilization history and suggests upsize/downsize actions. |
| 6 | Build vs buy: team lacks ML skills, tight deadline — default choice? | Buy (managed API/service, e.g., Vision API, Natural Language API) — avoids skill-gap risk and meets time-to-market pressure. Exam tip: organizational skill gaps push toward managed services. |
| 7 | TCO modeling — most commonly omitted cost category? | Indirect costs: staff retraining, migration labor, and ongoing operational overhead. Exam tip: a 'complete' TCO always includes these beyond raw infra pricing. |
| 8 | Regulated/risk-averse org change management — required control? | Staged rollout with mandatory manual approval gates and audit logging at each stage. Exam tip: continuous deployment without approval gates is the wrong answer in regulated scenarios. |
| 9 | Technical debt vs feature delivery — best stakeholder alignment approach? | Make risk/impact visible to stakeholders and negotiate a fixed % of sprint capacity for debt reduction (transparent trade-off), not silent work or full work stoppage. |
| 10 | Committed Use Discount minimum term options? | 1-year or 3-year terms only (no shorter/longer options exist for standard CUDs). Exam tip: 3-year gives largest discount but least flexibility. |
| 11 | Executive says 'reduce cost AND keep flexibility' — which discount mechanism fits both? | Sustained Use Discounts + Rightsizing Recommendations — automatic discount with no lock-in, combined with continuous machine-type optimization. |
| 12 | VMware Engine committed use discount scope? | CUDs for VMware Engine apply only to VMware Engine node commitments — they do not extend savings to standard Compute Engine, GKE, or Cloud Run usage. |

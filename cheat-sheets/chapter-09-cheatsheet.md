## Chapter 9 Cheat Sheet — Business Process, Stakeholder Management & Cost Optimization

### Discount Mechanisms Compared
| Type | Commitment | Discount (approx) | Flexibility | Best For |
|---|---|---|---|---|
| Resource-based CUD | 1yr / 3yr | ~37% / ~55% | Locked machine type/region | Stable, unchanging fixed workloads |
| Flexible (spend-based) CUD | 1yr / 3yr | Lower than resource-based | Spans Compute Engine, GKE, Cloud Run, Functions, VMware Engine | Mixed/varying service portfolios |
| Sustained Use Discount (SUD) | None | Up to 30% | Full flexibility | N1 machine types only, unpredictable usage |
| VMware Engine CUD | 1yr / 3yr | Discount off node price | Locked to VMware Engine nodes | VMware Engine only |

### Build vs Buy Decision Rule
- Team lacks required skill + tight deadline → **Buy** (managed API/service)
- Core differentiator + team has expertise + time available → **Build**
- Exam trap: choosing 'build' when the scenario states a skill gap and short deadline

### Rightsizing
- Tool: **Recommender API** (VM machine type recommender)
- Basis: 8/14/30-day CPU & memory utilization
- Action: upsize/downsize machine type automatically suggested

### TCO Modeling — Must Include
- Direct: compute, storage, network egress
- Indirect (commonly omitted): staff retraining, migration labor, ongoing ops overhead
- Exam trap: TCO comparisons that ignore indirect costs favor cloud unfairly

### Change Management (Regulated/Risk-Averse Orgs)
- Requires: staged rollout + **manual approval gates** + audit logging
- Wrong answers: continuous deployment, auto-promote canary, no-review feature flags

### Stakeholder Alignment
- Executive statement (e.g., "cut cost 30%, keep flexibility") must map to a **specific technical mechanism** — usually SUD + rightsizing, not a rigid multi-year CUD
- Technical debt vs feature pressure: negotiate **visible, fixed capacity allocation** (e.g., 20% of sprint) rather than silent work or full stoppage

### Exam Gotchas
1. Resource-based CUD ≠ transferable across machine families — picking it for a variable workload is a common wrong answer.
2. SUD only applies to N1 — don't assume it covers N2/E2/C2.
3. Flexible CUD trades discount % for cross-service applicability — pick it when service mix varies.
4. "Buy" is the safe default when a skill gap + time-to-market constraint both appear in a scenario.
5. TCO questions almost always test whether you included indirect/people costs, not just infra pricing.

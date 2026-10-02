## Chapter 8: Technical Process Optimization: SDLC, CI/CD & Troubleshooting — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Cloud Build default build timeout? | 10 minutes (600s) default; configurable up to 24 hours (86400s) via the `timeout` field in cloudbuild.yaml. Exam tip: long integration test suites need an explicit timeout increase. |
| 2 | Cloud Build free tier daily minutes? | 120 build-minutes/day free on the default machine type. Exam tip: relevant for cost-optimization scenario questions comparing CI/CD tooling. |
| 3 | Container Registry vs Artifact Registry in 2026? | Container Registry was deprecated and fully shut down in March 2025. Artifact Registry is the current service, supporting Docker, npm, Maven, Python, Go modules, Apt/Yum. Exam tip: any answer choosing Container Registry for a new pipeline is wrong. |
| 4 | What replaced Cloud Debugger? | Cloud Debugger was deprecated/shut down May 2023. Use Cloud Trace, Error Reporting, and Cloud Profiler for equivalent troubleshooting workflows. Exam tip: never select Cloud Debugger. |
| 5 | Cloud Deploy canary rollout mechanism? | Progressive percentage-based traffic shifting to a new revision (e.g., 10% → 50% → 100%) with configurable verification/approval phases. Exam tip: Cloud Deploy is the managed CD tool for GKE, Cloud Run, and Anthos. |
| 6 | Command to manually submit a Cloud Build job? | `gcloud builds submit --config=cloudbuild.yaml .` Exam tip: production pipelines typically use Cloud Build Triggers on repo push/PR events instead of manual submission. |
| 7 | Error Reporting vs Cloud Logging for triage? | Error Reporting auto-aggregates and groups stack traces with spike charts and new-error alerts. Cloud Logging requires manually built queries/filters. Exam tip: pick Error Reporting when the question emphasizes automatic grouping. |
| 8 | What problem does Binary Authorization solve? | Enforces that only images signed/attested by a trusted process (e.g., passed vulnerability scan) can be deployed to GKE or Cloud Run. Exam tip: correct answer for 'regulated environment needs verified image provenance before deploy.' |
| 9 | Blameless postmortem core principle? | Focus on systemic/process causes, not individual blame; produce timeline plus action items. Exam tip: any answer mentioning 'identify who caused it' or discipline is wrong. |
| 10 | Cloud Source Repositories free tier? | Free for up to 5 users per project, including 50GB storage and 50GB egress/month. Exam tip: additional users beyond 5 are billed per user/month. |
| 11 | Canary vs Blue/Green deployment? | Canary gradually shifts a small % of traffic to the new version while monitoring metrics before full rollout. Blue/Green switches 100% of traffic instantly between two full environments. Exam tip: canary = lower risk/slower; blue/green = fast rollback but requires double infrastructure. |
| 12 | Technical debt trade-off — exam framing? | Exam favors incremental repayment (fixed % of sprint capacity) over extremes like halting all feature work or ignoring debt indefinitely. Exam tip: look for balanced, incremental answers. |

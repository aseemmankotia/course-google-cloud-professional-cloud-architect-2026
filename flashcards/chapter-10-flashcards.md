## Chapter 10: Programmatic Interaction & Implementation Oversight — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | gcloud command group for GKE cluster management? | gcloud container (e.g., gcloud container clusters create). Exam tip: don't confuse with gcloud compute, which is for VMs/networking. |
| 2 | gcloud command group for VM/network/disk management? | gcloud compute. Exam tip: gcloud compute instances create, gcloud compute networks, gcloud compute disks all live here. |
| 3 | gcloud command group for managing service accounts and roles? | gcloud iam (e.g., gcloud iam service-accounts create, gcloud iam roles list). |
| 4 | How to switch between multiple gcloud project/environment settings safely? | gcloud config configurations create <name> then gcloud config configurations activate <name>. Exam tip: prevents accidental cross-project deployments. |
| 5 | Cloud Shell persistent storage amount? | 5GB persistent disk mounted at $HOME. Exam tip: files persist, but the shell VM session itself is ephemeral. |
| 6 | Cloud Shell inactivity disconnect time? | Approximately 20 minutes of inactivity disconnects the session. Exam tip: unsaved in-memory state (variables, running jobs) is lost. |
| 7 | Cloud Client Library vs REST/gRPC API vs gcloud CLI — when to use each? | gcloud/Cloud Shell = ad hoc/manual admin tasks. Cloud Client Libraries = idiomatic, production automation embedded in app code. Direct REST/gRPC = custom integrations, unsupported languages, or fine-grained control. |
| 8 | What does 'terraform plan' do for drift detection? | Compares desired config state against actual live infrastructure state and reports differences WITHOUT applying changes. Exam tip: always run plan before apply/reconcile. |
| 9 | What is the purpose of a design review checkpoint? | A scheduled validation point where the architect confirms implementation matches approved architecture before proceeding — catches drift early, before production cutover. |
| 10 | Best practice before production cutover of a new service? | Load/performance test + canary or staged rollout with defined automated rollback criteria in a pre-prod-like environment. Exam tip: avoid 100% traffic cutover without staged validation. |
| 11 | Legacy vs current recommended Google API client library approach? | google-api-python-client (discovery-based) = legacy, still functional. Cloud Client Libraries = current recommended, idiomatic, better typing/retry handling. |
| 12 | Key handoff artifact from architect to implementation/ops team? | Approved architecture diagram + requirements doc + design review sign-off; ops also needs runbooks/monitoring/alerting definitions for post-cutover operation. |

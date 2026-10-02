## Chapter 6: Identity, Access & Resource Hierarchy — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | GCP resource hierarchy order, top to bottom? | Organization > Folder > Project > Resource. IAM policies inherit downward as a union of allows; use Org Policy to restrict, since IAM alone cannot revoke an ancestor's grant. |
| 2 | Three types of IAM roles in GCP? | Primitive (Owner/Editor/Viewer/Browser — broad, legacy), Predefined (Google-curated, service-scoped), Custom (you define exact permissions). Exam tip: least privilege = predefined or custom, never primitive. |
| 3 | Where can custom IAM roles be created? | Organization or Project level only — NOT at Folder level. Common exam trap. |
| 4 | Org Policy constraint to block external IPs on Compute Engine VMs? | constraints/compute.vmExternalIpAccess — an allow/deny list guardrail applied at org/folder/project. |
| 5 | Org Policy constraint to prevent service account key creation? | constraints/iam.disableServiceAccountKeyCreation — pairs with Workload Identity to eliminate exported keys organization-wide. |
| 6 | Workload Identity Federation for GKE — what does it eliminate? | Exported/downloaded service account JSON keys. A Kubernetes ServiceAccount (KSA) is bound to a Google ServiceAccount (GSA) via roles/iam.workloadIdentityUser so pods call GCP APIs keylessly. |
| 7 | What expression language do IAM Conditions use? | CEL (Common Expression Language). Enables context-aware access using attributes like request.time and resource.name — e.g. auto-expiring temporary grants. |
| 8 | Service account key rotation best practice if user-managed keys are unavoidable? | Rotate every 90 days. Preferred alternative: avoid user-managed keys entirely — use Workload Identity or attached service accounts on Compute Engine/GKE. |
| 9 | How is the 'effective' IAM policy on a resource determined? | Union of the policy set on that resource plus all ancestor resources (Org, Folder, Project). Lower levels cannot revoke a higher-level grant via IAM alone — use Org Policy for restriction. |
| 10 | Default Compute Engine service account — exam gotcha? | By default it's granted roles/editor on the project — massive over-privilege. Exam expects disabling it and using a scoped custom service account instead. |
| 11 | roles/editor vs roles/storage.objectAdmin for object CRUD in one bucket — which is least privilege? | roles/storage.objectAdmin (predefined, scoped to Storage objects). roles/editor grants broad write access across almost all GCP services — a classic exam trap answer. |
| 12 | Folder design pattern for a multi-business-unit org with different compliance needs (e.g., EHR Healthcare)? | Create one folder per business unit/compliance boundary (e.g., Healthcare-HIPAA, Marketing). Apply Org Policy constraints at each folder so they inherit to all current and future projects nested inside. |

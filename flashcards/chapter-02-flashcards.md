## Chapter 2: Compute Selection & Migration Strategy — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Cloud Run: maximum configurable request timeout? | Up to 60 minutes (3600 seconds). Exam tip: default is 5 minutes — must be explicitly raised for long-running requests. |
| 2 | Cloud Run: maximum concurrent requests per container instance? | 1000. Exam tip: default concurrency is 80 — raise it for I/O-bound workloads to reduce instance count and cost. |
| 3 | MIG autoscaler default cooldown period? | 60 seconds. Exam tip: new instance startup metrics are excluded during cooldown, which can look like a scaling delay during spikes. |
| 4 | GKE Autopilot vs Standard — billing model? | Autopilot bills per-pod resource requests (vCPU/memory/storage). Standard bills per-node (VM), regardless of pod packing efficiency. |
| 5 | GKE Autopilot vs Standard — control tradeoff? | Autopilot: no node management, restricted privileged workloads, simplified ops. Standard: full node pool control, custom machine types, DaemonSets anywhere. |
| 6 | Cloud Run vs GKE — when to choose Cloud Run? | Stateless HTTP/event-driven containers, need scale-to-zero, no cluster management desired. Choose GKE when you need custom networking, StatefulSets, or fine-grained scheduling. |
| 7 | Migrate to Virtual Machines — what does it migrate and how? | Agentless replication of on-prem VMware, AWS EC2, or Azure VMs directly into Compute Engine with minimal downtime. Exam tip: this is the go-to service for 'lift-and-shift' datacenter migration scenarios. |
| 8 | 6 R's of migration — name the three tested most on the exam | Rehost (lift-and-shift, no code change), Replatform (minor optimization, e.g., move DB to Cloud SQL), Refactor/Re-architect (redesign into microservices). Exam tip: match keywords 'minimal changes' → rehost, 'redesign for scale' → re-architect. |
| 9 | Database Migration Service (DMS) — supported use case? | Minimal-downtime, continuous replication migration of MySQL, PostgreSQL, and SQL Server into Cloud SQL (or AlloyDB for PostgreSQL). Exam tip: choose DMS when the scenario says 'continuous replication until cutover.' |
| 10 | Compute selection decision tree — first branching question? | Does the workload need full control over the OS/infra? Yes → Compute Engine. No → containerized? Yes → GKE/Cloud Run branch. No → App Engine/Cloud Functions branch based on event vs. app model. |
| 11 | When should you choose Cloud Spanner over Cloud SQL during a database migration? | When the application needs horizontal scaling beyond a single region with strong consistency (global scale). Cloud SQL is capped to a single regional instance with read replicas; Spanner scales globally. |
| 12 | gcloud command to create a MIG with autoscaling based on CPU utilization | `gcloud compute instance-groups managed set-autoscaling my-mig --max-num-replicas=10 --target-cpu-utilization=0.6 --cool-down-period=60` |

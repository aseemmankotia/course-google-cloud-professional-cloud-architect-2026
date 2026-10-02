# Practice Test 2: Google Cloud Professional Cloud Architect (PCA) Prep

- **Questions:** 45
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A global trading platform requires an RPO of zero and an RTO under 60 seconds for its primary transactional database, and must remain fully available even if an entire GCP region fails. The team is evaluating database options for this tier. Which design BEST meets these requirements?

A) Cloud SQL for PostgreSQL with a cross-region read replica that is manually promoted during a regional outage
B) Cloud Bigtable with application-level replication configured between two regional clusters
C) Compute Engine instances running a self-managed database with regional persistent disks replicated synchronously across two zones
D) Cloud Spanner configured with a multi-region instance configuration (e.g., nam3) spanning three regions

---

**Q2.** A company needs a hybrid connection between its on-premises data center and GCP that meets a 99.99% availability SLA and supports 10 Gbps of dedicated, non-internet-routed bandwidth. Which configuration should the architect implement?

A) Two Dedicated Interconnect connections in different edge availability domains, each connected to a separate Cloud Router
B) A single Dedicated Interconnect connection terminated at one Cloud Router
C) A single HA VPN tunnel over the public internet with Cloud Router dynamic routing
D) A single Partner Interconnect connection provisioned through a service provider at 10 Gbps

---

**Q3.** A retailer runs a monolithic Java application on VMware with tightly coupled dependencies on the local file system and JVM configuration. The business has an 8-week deadline to exit the on-premises data center due to a lease expiration, and the team has no bandwidth to refactor the application before the deadline. Which migration approach should the architect recommend?

A) Refactor the application into microservices and deploy to Google Kubernetes Engine
B) Rewrite the application as a set of Cloud Run services to eliminate infrastructure management
C) Use Migrate to Virtual Machines to lift-and-shift the VMware VMs directly to Compute Engine
D) Deploy Anthos on-premises to modernize the application in place without migrating it to GCP

---

**Q4.** An organization uses a hub-and-spoke Shared VPC design with one host project and five service projects, each owned by a different application team. The security team requires that each team can only launch VM instances into the specific subnets assigned to their team, without being able to modify firewall rules or subnet configurations in the host project. Which configuration meets this requirement?

A) Grant each team's group the Compute Network Admin role on the host project
B) Create a separate VPC per team and connect all VPCs to the host VPC using VPC Peering
C) Grant each team's group the Project Owner role on the host project so they can self-manage networking
D) Grant each team's group the Compute Network User role scoped to their specific subnets in the host project

---

**Q5.** A workload runs continuously 24/7 with a stable baseline of 200 vCPUs for a committed 3-year period, plus unpredictable traffic bursts of up to 100 additional vCPUs a few times per month. The architect must minimize cost while keeping the burst capacity flexible. Which combination of purchasing options should be used?

A) Apply sustained use discounts to all 300 vCPUs and rely on their automatic monthly application
B) Purchase a 3-year resource-based Committed Use Discount for the 200 vCPU baseline, and use on-demand autoscaled instances for the burst capacity
C) Purchase Reserved Instances for the full 300 vCPUs to lock in the lowest possible rate
D) Run all 300 vCPUs on Spot VMs to take advantage of the deepest available discount

---

**Q6.** A financial services company must migrate its on-premises Oracle database to GCP with minimal application changes and near-zero downtime during cutover, ideally landing on a fully managed, PostgreSQL-compatible destination. Which migration approach should the architect choose?

A) Use Storage Transfer Service to move nightly Oracle export dumps into Cloud Storage, then load them into Cloud SQL
B) Write custom scripts on a Compute Engine VM to poll Oracle redo logs and replicate changes into Cloud SQL
C) Use Database Migration Service to perform a continuous, CDC-based migration from Oracle to AlloyDB for PostgreSQL
D) Use Datastream alone to stream Oracle data continuously into BigQuery for the application to query directly

---

**Q7.** A retail company runs 400 VMware VMs on-premises and wants to migrate them to Compute Engine with the least possible cutover downtime. They want to validate application behavior in an isolated network before the final cutover, and they want continuous block-level replication so the cutover delta is minimal. Which migration approach should the architect recommend?

A) Export each VM to OVA format, upload the images to Cloud Storage, and create custom Compute Engine images from the OVA files
B) Use the Transfer Appliance to ship VM disk data to Cloud Storage, then import the disks with gcloud compute images import
C) Use Migrate to Virtual Machines to replicate the VMs continuously, run them as test clones in an isolated network for validation, then cut over
D) Use Migrate for Anthos to convert the VMs into containers and deploy them on GKE before validating in a staging cluster

---

**Q8.** A hospital network needs a hybrid connection from its on-premises data center to a VPC, requiring a 99.99% availability SLA and 10 Gbps of dedicated capacity. The hospital's IT team does not have equipment co-located in any Google-supported colocation facility and does not want to establish a physical presence there. Which connectivity option satisfies these requirements?

A) Partner Interconnect with connections through two different service provider edge availability domains
B) Dedicated Interconnect with a single 10 Gbps connection
C) Cross-Cloud Interconnect to establish direct connectivity to the on-premises network
D) Classic Cloud VPN with two tunnels configured in an active-active HA VPN setup

---

**Q9.** A global financial trading platform requires a transactional database with near-zero RPO and automatic failover in under a minute across three regions, while maintaining strong consistency for all reads and writes. Which Google Cloud database service should the architect select?

A) Cloud SQL for PostgreSQL with a cross-region read replica promoted manually during failover
B) Cloud Spanner configured with a multi-region instance configuration
C) Cloud Bigtable configured with multi-cluster routing across three regions
D) Memorystore for Redis with cross-region replication enabled

---

**Q10.** A company runs a stable, predictable workload requiring a fixed set of specific N2 machine type vCPUs and memory continuously for the next 3 years. The finance team wants to guarantee the maximum possible discount and is willing to commit to that exact resource footprint regardless of whether usage fluctuates slightly month to month. Which pricing model should the architect recommend?

A) Rely on automatic Sustained Use Discounts, since usage already exceeds 25% of the month
B) Use Spot VMs for the workload to take advantage of the deepest available discounts
C) Purchase a 1-year Flexible Committed Use Discount based on projected monthly spend
D) Purchase a 3-year resource-based Committed Use Discount for the specific N2 machine type resources

---

**Q11.** A large enterprise has 20 independent application teams, each requiring its own project for IAM isolation and separate billing, but the network security team must centrally manage all firewall rules, subnets, and a single Dedicated Interconnect connection to the on-premises data center shared by all teams. Which network design should the architect implement?

A) Create individual VPCs per team and connect them all to each other using VPC Network Peering
B) Create individual VPCs per team and connect each to on-premises using its own Cloud VPN tunnel
C) Create a Shared VPC with the network team's project as the host project and each team's project attached as a service project
D) Consolidate all 20 teams into a single project and assign each team a distinct IAM role

---

**Q12.** A company uses Shared VPC with a host project 'net-host' and two service projects, 'team-a-svc' and 'team-b-svc'. Team A's project admins need to create and manage firewall rules that apply only to instances tagged 'team-a-web' in the Shared VPC network, without being able to view or modify firewall rules that affect Team B's resources. Which approach BEST meets this requirement?

A) Grant Team A's admins the Compute Security Admin role on the host project net-host, scoped with an IAM condition that restricts the grant to firewall rule resources containing the target tag 'team-a-web'.
B) Grant Team A's admins the Owner role on their own service project team-a-svc.
C) Grant Team A's admins the Compute Network User role on the host project net-host.
D) Create a separate VPC network for Team A and connect it to the Shared VPC network using VPC Network Peering.

---

**Q13.** An organization has three VPC networks: vpc-finance, vpc-hr, and vpc-shared-services. vpc-finance is peered with vpc-shared-services, and vpc-hr is also peered with vpc-shared-services. A new requirement states that instances in vpc-finance must reach internal load balancers in vpc-hr using internal IP addresses, and the organization expects to add several more department VPCs with similar cross-communication needs in the near future. Which solution BEST meets these requirements with minimal ongoing management overhead?

A) Rely on the existing peering configuration, since VPC Network Peering is transitive and vpc-finance can already reach vpc-hr through vpc-shared-services.
B) Migrate the department VPCs to a Shared VPC architecture with a single host project, or adopt Network Connectivity Center in a hub-and-spoke topology.
C) Create a direct VPC Network Peering connection between vpc-finance and vpc-hr.
D) Configure Cloud VPN tunnels between vpc-finance and vpc-hr using their internal RFC 1918 IP ranges.

---

**Q14.** A batch-processing workload runs on Compute Engine instances that have no external IP addresses. The instances must read objects from Cloud Storage and must also download base container images from Docker Hub on the public internet during startup. Which configuration is required to satisfy both requirements?

A) Configure a Cloud NAT gateway on the subnet only.
B) Enable Private Google Access on the subnet only.
C) Temporarily assign external IP addresses to the instances during the startup phase.
D) Enable Private Google Access on the subnet AND configure a Cloud NAT gateway.

---

**Q15.** A platform team already manages all Kubernetes workloads through GitOps: manifests are stored in a Git repository and reconciled onto GKE clusters by a continuous delivery operator. They now want to provision GCP resources, such as Cloud SQL instances and Cloud Storage buckets, using the same GitOps workflow and the same kubectl-based tooling, with the resources' state visible through the Kubernetes API alongside their application objects. Which tool should they use to provision the GCP resources?

A) Cloud Deployment Manager.
B) Terraform with the Google provider, applied through a separate CI/CD pipeline outside of Kubernetes.
C) gcloud CLI scripts triggered by Cloud Build on every Git push.
D) Config Connector.

---

**Q16.** A team uses Cloud Build to build container images and wants a fully managed continuous delivery pipeline that automatically deploys new releases to a staging GKE cluster, then requires an explicit manual approval before that same release is promoted to the production GKE cluster. Which approach implements this promotion workflow with a built-in approval gate?

A) Configure two separate Cloud Build triggers, one for staging and one for production, each firing independently on push to a branch.
B) Use Google Cloud Deploy to define a delivery pipeline with staging and production targets, enabling a required approval on the production target.
C) Use Cloud Scheduler to invoke the production Cloud Build trigger a fixed number of hours after the staging deployment completes.
D) Store images in Artifact Registry and use a Cloud Function triggered on new image push to deploy directly to production.

---

**Q17.** A company requires a hybrid connection between its on-premises data center and its VPC network with these requirements: 10 Gbps aggregate throughput, traffic that never traverses the public internet, and a 99.99% availability SLA. Which configuration BEST meets these requirements?

A) Two Dedicated Interconnect connections, each in a different Interconnect location, configured with redundant Cloud Routers.
B) A single Dedicated Interconnect connection with 10 Gbps of capacity.
C) Two Dedicated Interconnect connections in the same metro location but attached to different edge availability domains.
D) A Partner Interconnect connection combined with a Cloud VPN tunnel configured as an automatic failover path.

---

**Q18.** A company's Shared VPC host project "host-prod" connects to on-premises data centers via Dedicated Interconnect using a Cloud Router with dynamic (BGP) routing. Separately, host-prod has a VPC Network Peering connection to a partner organization's VPC, "partner-vpc", established for a joint analytics workload. The partner now needs their VMs in partner-vpc to reach on-premises database servers through the existing peering connection to host-prod. Which approach correctly enables this connectivity, consistent with how Google Cloud VPC Network Peering handles routes?

A) VPC Network Peering is fully transitive for all routes, so no additional configuration is needed — partner-vpc VMs already have access to the on-premises routes
B) Manually create a static route in partner-vpc with the on-premises CIDR as the destination and the peering connection configured as the next hop
C) Replace the existing VPC Network Peering connection with a direct Cloud VPN tunnel between partner-vpc and host-prod to carry the on-premises routes
D) Enable custom route export on host-prod's side of the peering connection and custom route import on partner-vpc's side, so the on-premises routes learned dynamically via Cloud Router are shared with partner-vpc

---

**Q19.** A financial services company stores sensitive datasets in BigQuery within a shared VPC across multiple projects. Security team must prevent any GCP identity from copying data out of the org's BigQuery datasets into external projects or exporting it, while still permitting an on-premises fraud-detection application (connected via Dedicated Interconnect) to query the data. Which approach BEST meets these requirements?

A) Configure IAM Conditions on the BigQuery datasets to restrict the bigquery.tables.export permission for all users
B) Create a VPC Service Controls perimeter around the projects containing the BigQuery datasets, with an access level that requires the corporate on-prem IP range reachable via Interconnect
C) Enable Cloud DLP inspection jobs on the datasets to automatically redact sensitive fields before queries run
D) Apply an Organization Policy constraint restricting the allowed resource locations for the datasets

---

**Q20.** A healthcare organization must use encryption keys that are generated and remain stored entirely within their own on-premises hardware security module (HSM), while still allowing Google Cloud services such as BigQuery and Compute Engine to perform encryption operations using those keys via API calls. Google must never have access to the raw key material at any point. Which key management approach should the architect select?

A) Cloud External Key Manager (Cloud EKM) integrated with a supported external key management partner
B) Customer-managed encryption keys (CMEK) using Cloud KMS
C) Customer-supplied encryption keys (CSEK) passed with each API request
D) Google-managed default encryption at rest

---

**Q21.** An architect wants to enforce, at the organization level, that no Compute Engine VM instance anywhere in the resource hierarchy can ever be assigned an external (public) IP address, with no project able to override this. Which Organization Policy constraint should be enforced?

A) constraints/compute.vmExternalIpAccess set to deny all
B) constraints/compute.requireOsLogin
C) constraints/compute.restrictVpcPeering
D) constraints/iam.disableServiceAccountKeyCreation

---

**Q22.** A DevOps team runs its CI/CD pipeline in GitHub Actions and needs to deploy resources to Google Cloud. The security team mandates that no long-lived service account keys may be downloaded or stored as CI/CD secrets. Which solution allows GitHub Actions to authenticate to Google Cloud securely while meeting this requirement?

A) Generate a service account key, base64-encode it, and store it as an encrypted GitHub Actions secret
B) Configure Workload Identity Federation to establish trust between GitHub's OIDC token issuer and a Google Cloud service account, exchanging short-lived tokens
C) Grant the GitHub Actions runner's static IP address access through a firewall rule and authenticate using a shared service account password
D) Use Identity-Aware Proxy to allow unauthenticated access from GitHub's published IP ranges

---

**Q23.** Before loading customer support chat transcripts into BigQuery for analytics, a company needs to automatically identify and mask credit card numbers, email addresses, and phone numbers embedded in free-form text, without manually writing regex patterns for every possible format. Which Google Cloud service should be used in the data pipeline?

A) Cloud Data Loss Prevention (Cloud DLP) API using built-in infoType detectors
B) Cloud Armor with custom WAF rules
C) BigQuery column-level security using policy tags
D) Cloud KMS envelope encryption applied to the entire transcript field

---

**Q24.** An architect is designing IAM policies for a large enterprise with hundreds of engineers across dozens of teams. Following least-privilege best practices, which approach should be used to grant engineers only the permissions they need for their job function, avoiding both overly broad primitive roles and the excessive maintenance overhead of building fully custom roles for every function?

A) Grant the primitive Editor role to every engineer at the project level, since it covers most day-to-day needs
B) Assign predefined IAM roles that closely map to job functions (e.g., roles/bigquery.dataViewer, roles/compute.instanceAdmin.v1), reserving custom roles only for specific gaps
C) Create a fully custom IAM role for every distinct job function across the organization
D) Grant the Owner role to all engineers but restrict its effect using Organization Policy constraints

---

**Q25.** A healthcare company's BigQuery datasets and Cloud Storage buckets span 12 projects inside a single GCP organization. A compliance audit requires that no user or service, even one with valid IAM permissions on the resources, can copy or export regulated data to any resource outside the organization's projects. Analysts must still be able to run cross-project queries within the org, and a research team connecting from an on-premises data center over Cloud Interconnect must retain query access. Which design meets these requirements?

A) Apply the Organization Policy constraint iam.allowedPolicyMemberDomains to block granting IAM roles to external identities, and rely on default IAM permissions for cross-project queries
B) Enable Cloud DLP inspection templates on all BigQuery datasets to automatically redact sensitive fields before any export job can complete
C) Create a single VPC Service Controls perimeter containing all 12 projects, define an access level scoped to the on-prem IP range and corporate device policy for Interconnect access, and let the perimeter block API calls that would move data to resources outside it
D) Enable customer-managed encryption keys (CMEK) via Cloud KMS on every BigQuery dataset and Cloud Storage bucket so that only key-holders in the org can decrypt exported data

---

**Q26.** A company's CI/CD pipeline runs on GitHub Actions and needs to deploy resources to a GCP project. The security team's compliance policy prohibits storing any long-lived, downloadable service account keys anywhere, including in secret managers, and requires that all machine-to-machine authentication to GCP be short-lived and auditable per pipeline run. Which configuration satisfies this requirement?

A) Configure Workload Identity Federation to trust GitHub Actions' OIDC token issuer, mapping specific repository/branch claims to permission to impersonate a dedicated GCP service account with no key ever created
B) Generate a service account key, store it as an encrypted GitHub Actions secret, and configure a Cloud Scheduler job to rotate the key automatically every 24 hours
C) Deploy Identity-Aware Proxy in front of the deployment target and require the pipeline to authenticate through the IAP OAuth consent flow using a shared client secret
D) Create a service account key, store it in Secret Manager with a 90-day expiration label, and configure an IAM Conditions policy that denies use of the key after 90 days

---

**Q27.** After a major production outage, a Cloud Architect is asked to design the incident review process going forward. The goal is to determine root cause accurately, avoid repeat incidents, and maintain team trust so future issues are reported quickly. Which approach best achieves this?

A) Have engineering leadership hold a closed-door meeting to identify which individual caused the outage and note it in their performance review
B) Skip formal documentation since the incident was resolved within the SLA window, relying on the team's Slack history as the record
C) Have the on-call SRE write a purely technical log summary with no stakeholder communication or action-item tracking
D) Conduct a blameless postmortem documenting the incident timeline, contributing factors, customer impact, and specific remediation action items with owners and due dates, then track them to closure

---

**Q28.** A company with a 3-person platform team must retain application logs for 2 years to satisfy compliance audits and support ad hoc analytical queries from the compliance team. Which approach best balances time-to-value and total cost of ownership?

A) Build and operate self-managed Elasticsearch clusters on Compute Engine to retain full control over indexing and query performance
B) Store raw logs in Cloud Storage and write a new custom Dataflow job every time the compliance team requests a different query pattern
C) Have the platform team develop a proprietary log indexing and search engine in-house to avoid recurring vendor costs
D) Route logs through Cloud Logging, configure a log sink to export them to BigQuery, and use standard SQL for compliance reporting and ad hoc analysis

---

**Q29.** A financial services company must satisfy regulatory requirements for documented, auditable approval of every production change while also increasing deployment frequency. Which process should the architect recommend?

A) Implement a CI/CD pipeline in Cloud Build with automated testing, a required manual approval gate before the production deployment step, and Binary Authorization to enforce that only attested, policy-compliant container images can deploy
B) Continue quarterly release cycles where every change, regardless of risk, is manually reviewed by a change advisory board (CAB) before release
C) Allow developers to deploy directly to production using gcloud, relying on Cloud Audit Logs for after-the-fact review
D) Route every code change through the CFO for manual sign-off before it can be merged, since this is a regulated financial company

---

**Q30.** Utilization analysis shows a workload has a stable baseline of 20 vCPUs running continuously plus predictable business-hours bursts up to 60 vCPUs. Which cost optimization strategy best fits this pattern?

A) Purchase a 1-year Committed Use Discount sized for the full 60 vCPU peak and run that capacity flat at all times
B) Purchase a 1-year Committed Use Discount for the 20 vCPU baseline, and configure a managed instance group with autoscaling to burst up to 60 vCPUs on-demand during peak hours
C) Run the entire workload on preemptible/Spot VMs to minimize cost, regardless of the workload's availability requirements
D) Avoid any commitment and pay on-demand pricing continuously for the full 60 vCPU peak capacity to preserve maximum flexibility

---

**Q31.** Product management is pushing for rapid feature delivery while the engineering team reports that accumulating technical debt in the monolithic application is slowing development and increasing incident rates. Which recommendation best balances these competing priorities?

A) Halt all new feature development for two quarters to fully rewrite the monolith as microservices before resuming feature work
B) Ignore the technical debt concerns and dedicate all engineering capacity to new features to meet business deadlines
C) Establish a policy reserving a fixed percentage of each sprint's capacity for addressing critical technical debt items, prioritized by risk and incident impact, while continuing incremental feature delivery
D) Let individual engineers refactor code informally whenever they have spare time, without tracking debt items or measuring their impact

---

**Q32.** An organization's engineering teams are siloed strictly by technical function (frontend, backend, operations) with no cross-training, and management wants to migrate the monolithic application to a microservices architecture. Which recommendation best reflects sound architectural guidance given the organizational constraints?

A) Migrate immediately to a fully decomposed microservices architecture, since this is considered current best practice regardless of team structure
B) Recommend reorganizing engineering into small, cross-functional teams aligned to service boundaries before or alongside decomposition, and provide targeted training, since system architecture tends to mirror organizational communication structures
C) Keep the monolith unchanged indefinitely, since reorganizing engineering teams falls outside a cloud architect's scope of responsibility
D) Outsource the entire migration to a third-party contractor without involving internal teams, since the existing team structure cannot realistically change

---

**Q33.** An organization has adopted Google's SRE practices, including formal error budgets tied to a 99.9% availability SLO for a customer-facing API. This quarter, three separate production incidents caused by rushed deployments consumed the entire error budget by the second month of the quarter. Engineering leadership wants a recommendation that is consistent with SRE error budget policy and the organization's stated goal of balancing reliability with delivery speed. Which action should the cloud architect recommend?

A) Raise the SLO target to 99.5% so future minor incidents no longer exhaust the error budget as quickly
B) Halt new feature releases for the API and redirect the team's effort to reliability work until the error budget is restored
C) Require the on-call engineer responsible for the most recent deploy to complete a formal disciplinary review before any further releases are approved
D) Continue the existing release cadence since the product roadmap commitments to customers take priority over the internal error budget metric

---

**Q34.** A retail company runs its CI/CD pipeline on a self-managed Jenkins cluster hosted on Compute Engine. The two-person platform team spends over 50% of its time patching Jenkins plugins for recurring CVEs and manually scaling build agents during peak release periods. Business stakeholders have set a goal of cutting time-to-market for new features by 40% this year, but the company has no budget approved to grow the platform team. Which change best optimizes the technical process while respecting the stated business and staffing constraints?

A) Migrate the pipeline to a Google Cloud managed CI/CD service such as Cloud Build, removing the operational burden of patching and scaling the underlying build infrastructure
B) Re-architect Jenkins to run on a self-managed GKE cluster so build agents can autoscale more elastically than on Compute Engine VMs
C) Request approval to hire two additional DevOps engineers dedicated to patching Jenkins plugins and managing agent capacity
D) Introduce a formal change advisory board that reviews and approves every Jenkins plugin update before it is applied to production

---

**Q35.** A team uses Cloud Deploy to progressively roll out a new microservice version across dev, staging, and prod GKE clusters. During the canary phase in prod, they want the rollout to automatically halt and roll back if the service's error rate exceeds an SLO threshold defined in Cloud Monitoring — without any human intervention. Which approach BEST satisfies this requirement?

A) Configure the GKE Horizontal Pod Autoscaler to automatically remove pods that report HTTP 500 responses during the canary phase.
B) Add a postdeploy hook to the canary phase that queries Cloud Monitoring for the error-rate SLO and fails the phase if it is breached, combined with Cloud Deploy's rollback-on-failure setting.
C) Create a nightly Cloud Build trigger that redeploys the previous stable container image to production.
D) Have the on-call engineer watch the Cloud Monitoring dashboard during the rollout and manually trigger a rollback from the console if needed.

---

**Q36.** A platform team wants to manage core GCP infrastructure (VPCs, subnets, IAM policy bindings) using Kubernetes-style YAML manifests that are continuously reconciled by a controller running inside a GKE cluster, fitting into an existing GitOps workflow. Which tool should they use?

A) Cloud Deployment Manager
B) Terraform Cloud with manual apply approvals
C) Cloud Asset Inventory with a Pub/Sub feed
D) Config Connector (KCC) running in the GKE cluster

---

**Q37.** Multiple engineers on a team run Terraform against the same GCP project. They occasionally run 'terraform apply' at the same time, resulting in corrupted state files. Which change to their Terraform configuration BEST prevents this going forward?

A) Store the Terraform state file in a version-controlled Git repository alongside the configuration files.
B) Migrate the state to a Cloud SQL for PostgreSQL instance and use row-level locks.
C) Configure a GCS bucket as the Terraform backend; the GCS backend natively provides state locking to prevent concurrent applies.
D) Switch from Terraform to Cloud Deployment Manager, which does not require external state locking.

---

**Q38.** An architecture team suspects engineers have been making manual changes to a GKE cluster's configuration directly through the Cloud Console, causing drift from the Terraform-managed definition. Which approach BEST detects and systematically prevents this drift going forward?

A) Enable a Cloud Asset Inventory feed to log all IAM and resource changes for later auditing.
B) Switch the cluster to GKE Autopilot mode so Google manages all node-level configuration.
C) Instruct engineers to notify the platform team by email whenever they make a manual change in the console.
D) Schedule terraform plan to run in a CI pipeline on a recurring basis to detect drift, and restrict direct edit permissions on the cluster to the automation service account only.

---

**Q39.** An architect wants to deploy a new App Engine service version so it can be validated at its version-specific URL before any production traffic is routed to it. Which gcloud app deploy flag achieves this?

A) --quiet
B) --stop-previous-version
C) --no-promote
D) --version=v2

---

**Q40.** A company has an SLO of 99.95% availability for its public API measured over a rolling 28-day window. Monitoring shows the current burn rate will exhaust the entire error budget in 3 days. The product team wants to ship a major new feature this week that adds significant new code paths to the same service. What should the architect recommend?

A) Halt non-critical feature launches and prioritize reliability engineering work until the error budget recovers
B) Redefine the SLI measurement window from 28 days to 90 days to reset the error budget calculation
C) Proceed with the launch since the current availability still satisfies the customer-facing SLA, which is lower than the SLO
D) Increase the SLO target to 99.99% availability to create additional error-budget headroom for future incidents

---

**Q41.** A critical OLTP workload currently runs on a single-region Cloud SQL for PostgreSQL instance. The business now requires an RPO of 5 minutes and an RTO of 15 minutes in the event of a full regional outage, with minimal ongoing operational overhead. Which approach best meets these requirements?

A) Configure a cross-region read replica for Cloud SQL and manually promote it during a regional outage
B) Rely on Cloud SQL automated backups with point-in-time recovery restored to a new instance in another region
C) Migrate the workload to Cloud Spanner configured as a multi-region instance
D) Set up a nightly cross-region database dump-and-restore process to a standby Cloud SQL instance

---

**Q42.** A microservices application running on GKE experiences intermittent high latency on certain user requests. The team needs to visualize the full request path across multiple services and pinpoint exactly which downstream service call is adding the delay. Which tool should they use?

A) Enable Cloud Profiler on each microservice to capture CPU and memory usage
B) Configure Cloud Monitoring dashboards with aggregated custom latency metrics per service
C) Instrument the services with Cloud Trace to visualize per-request latency across the call graph
D) Enable structured JSON logging in Cloud Logging and correlate log entries by request ID manually

---

**Q43.** A team runs several services on App Engine and Cloud Run. They want unhandled exceptions from all services automatically aggregated and grouped by root cause (deduplicating identical stack traces) and to be notified when a new error type first appears. Which Google Cloud tool is designed specifically for this?

A) Error Reporting
B) Cloud Trace
C) Cloud Logging log-based metrics with alerting policies
D) Security Command Center

---

**Q44.** An architect needs to configure a canary release for a service running on GKE, routing approximately 5% of traffic to the new version. No service mesh (such as Istio/Anthos Service Mesh) is installed, and native Kubernetes objects must be used. Which configuration achieves this?

A) Run kubectl rollout pause on the existing Deployment update to hold 5% of pods on the new revision
B) Create a separate Ingress resource routing to a canary namespace
C) Deploy the new version as a separate Deployment sharing the same Service label selector as the stable Deployment, and scale replica counts to approximate a 5% traffic ratio
D) Configure a HorizontalPodAutoscaler to scale the canary Deployment to 5% of total replicas based on CPU utilization

---

**Q45.** A production outage was caused by an engineer making a manual configuration change directly in production without following the documented change-management process. During the post-incident review, which action best aligns with Google's SRE blameless postmortem culture?

A) Identify the engineer who made the unauthorized change and issue a formal written reprimand
B) Restrict production deployment access to only senior engineers going forward
C) Document the incident internally only if it breached the SLA, and keep the report private since it was resolved quickly
D) Focus the review on the systemic process and tooling gaps that allowed an unreviewed change to reach production, and implement automated safeguards

---


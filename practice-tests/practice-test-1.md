# Practice Test 1: Google Cloud Professional Cloud Architect (PCA) Prep

- **Questions:** 45
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A financial services company runs a critical PostgreSQL database and must meet an RPO of 15 minutes and an RTO of 1 hour in case of a regional outage. The operations team wants a fully managed solution with minimal operational overhead to configure and maintain. Which approach BEST meets these requirements?

A) Run self-managed PostgreSQL on Compute Engine and take persistent disk snapshots every 4 hours for cross-region recovery
B) Configure Cloud SQL automated backups only and restore from the latest backup in the event of a regional outage
C) Export the database to Cloud Storage nightly and re-import it into a new Cloud SQL instance in another region during failover
D) Use Cloud SQL for PostgreSQL with a cross-region read replica that can be promoted to a standalone primary during failover

---

**Q2.** A company needs to connect its on-premises data center to its Google Cloud VPC with a dedicated 10 Gbps link, low and predictable latency, and a requirement that traffic never traverse the public internet. The company has the ability to co-locate equipment at a facility with direct access to Google's network. Which connectivity option should be selected?

A) HA VPN over the public internet
B) Cloud NAT with static outbound IP addresses
C) Dedicated Interconnect
D) Partner Interconnect through a service provider

---

**Q3.** A company runs a legacy Java monolith on VMware on-premises and must move it to Google Cloud within 3 months due to a data center contract expiration. Leadership wants to eventually modernize the application into microservices, but the immediate priority is meeting the deadline with minimal risk. Which migration approach should be used first?

A) Rewrite the application from scratch using App Engine Standard before migrating
B) Immediately re-architect the monolith into containerized microservices deployed on GKE
C) Manually export VM disk images and recreate the instances using custom Deployment Manager templates
D) Use Migrate to Virtual Machines to lift-and-shift the VMs to Compute Engine, then modernize incrementally afterward

---

**Q4.** An organization has separate GCP projects for its dev, prod, and data-analytics teams. Each team must retain its own billing and IAM boundaries, but the network security team wants to centrally manage VPC network topology, subnets, and firewall rules across all three projects. Which network design should be used?

A) Establish VPC Peering connections between all three projects' independent VPC networks
B) Consolidate all three teams into a single GCP project with IAM roles separating access
C) Deploy a separate VPC network per project and connect them using a full mesh of Cloud VPN tunnels
D) Configure a Shared VPC with a host project managed by the network security team and attach each team's project as a service project

---

**Q5.** A team needs to deploy a stateless HTTP microservice packaged as a custom Docker container image with a non-standard runtime not supported by Google's buildpacks. The service must scale to zero when idle and support request timeouts of up to 60 minutes. Which compute service should be used?

A) Cloud Run
B) App Engine Standard environment
C) GKE Autopilot cluster
D) Cloud Functions (2nd gen)

---

**Q6.** A company runs a steady-state batch analytics workload on Compute Engine that must run continuously 24/7 for the next 3 years with predictable, unchanging resource requirements. The workload cannot tolerate interruption. Which purchasing option minimizes cost while meeting these constraints?

A) Rely only on automatically applied sustained use discounts
B) Purchase a 3-year Committed Use Discount for the required vCPUs and memory
C) Run the workload entirely on Spot VMs to take advantage of the lowest hourly rate
D) Use standard on-demand pricing to retain full billing flexibility

---

**Q7.** A company requires a disaster recovery solution for their financial transaction database with an RPO of 15 minutes and RTO of 1 hour. The database currently runs on Cloud SQL for PostgreSQL in us-central1. Which solution BEST meets these requirements?

A) Configure a cross-region read replica in us-east1 and promote it to a standalone primary instance during a disaster
B) Enable automated backups with 7-day retention and restore to a new instance in another region during a disaster
C) Export nightly database dumps to Cloud Storage and use Cloud Storage multi-region for redundancy
D) Migrate the database to Cloud Spanner configured as a single-region instance

---

**Q8.** A retail company needs to connect their on-premises data center to Google Cloud with a guaranteed SLA, requires 10 Gbps of dedicated bandwidth, and cannot route traffic over the public internet due to compliance requirements. Which connectivity option should the architect choose?

A) Cloud VPN using HA VPN gateways
B) Dedicated Interconnect
C) Direct Peering
D) Partner Interconnect with a 1 Gbps connection

---

**Q9.** A company must migrate 200 on-premises VMware VMs running a legacy ERP application to Google Cloud within a 6-week deadline. The application vendor does not support containerization, and the operations team wants to minimize changes to the OS and application configuration. Which migration approach should the architect recommend?

A) Use Migrate to Virtual Machines to lift-and-shift the VMs to Compute Engine
B) Re-architect the application to run on Google Kubernetes Engine using Migrate to Containers
C) Manually export each VM as an OVA file and import them individually using Cloud Storage transfer
D) Rewrite the application as a set of Cloud Functions

---

**Q10.** An architecture team is designing a fleet of Compute Engine VMs that will run continuously for 3 years with predictable, stable usage, and they are willing to commit to that usage level in advance to minimize compute costs. Which pricing model should they choose?

A) 3-year committed use discount (resource-based)
B) Sustained use discounts
C) Spot VMs
D) On-demand pricing with no discounts

---

**Q11.** Which statement correctly differentiates Cloud Run from Google Kubernetes Engine (GKE) Autopilot for deploying containerized workloads?

A) Cloud Run requires the customer to manage the underlying node pool, whereas GKE Autopilot is fully serverless with no infrastructure to manage
B) GKE Autopilot scales to zero running instances by default, while Cloud Run always maintains a minimum of one running instance
C) Cloud Run only supports HTTP-triggered services, while GKE Autopilot only supports gRPC workloads
D) Cloud Run is a fully managed serverless platform billed per request/duration, while GKE Autopilot is a managed Kubernetes environment billed per pod resource requests, offering more control over networking and stateful workloads

---

**Q12.** A company has a central networking team that must control all subnets, routes, and firewall rules, while separate application teams (dev, test, prod) need to deploy Compute Engine and GKE resources into isolated projects without networking privileges. The application teams' resources must still communicate over private RFC 1918 IP space. Which topology BEST meets these requirements?

A) Create separate VPCs per team and connect them using VPC Peering
B) Create a Shared VPC with the networking team owning the host project and each application team's project attached as a service project
C) Give each application team its own VPC and connect them with a full-mesh Cloud VPN
D) Put all resources in a single project with one VPC and use IAM conditions to restrict firewall edits

---

**Q13.** A data engineering team ingests 50 TB of clickstream events daily and needs to run ad-hoc SQL analytics across the full historical dataset with minimal operational overhead and no need to manage servers or storage capacity in advance. Which Google Cloud service should they use?

A) Cloud Bigtable
B) BigQuery
C) Cloud SQL for PostgreSQL
D) Persistent Disk with a Compute Engine-hosted data warehouse

---

**Q14.** Compute Engine VMs in a private subnet have no external IP addresses but need to pull container images from Artifact Registry and read objects from Cloud Storage without traversing the public internet. What must you configure to enable this?

A) Deploy a Cloud NAT gateway for the subnet
B) Enable Private Google Access on the subnet
C) Set up VPC Peering to Google's default network
D) Configure Serverless VPC Access connector for the subnet

---

**Q15.** A retailer already has network equipment installed in a colocation facility that offers direct access to a Google Cloud edge availability zone. They need a 10 Gbps private connection to their VPC with an SLA of 99.99% availability and no data traversing the public internet. Which connectivity option should they choose?

A) Dedicated Interconnect
B) Classic VPN with static routing
C) Direct Peering
D) Carrier Peering

---

**Q16.** An architect is deciding between Cloud Deployment Manager and Terraform for provisioning a Google Cloud environment that must eventually be extended to manage some resources in a secondary cloud provider. What is a key advantage of Terraform in this scenario?

A) Terraform is a Google-proprietary tool that only supports Google Cloud resources
B) Deployment Manager natively supports multi-cloud providers while Terraform does not
C) Terraform requires no state tracking because it queries live infrastructure on every run
D) Terraform uses declarative configuration files and a state file to track resources across multiple providers, including non-Google clouds

---

**Q17.** A team wants every push to the main branch of their GKE application repository to automatically build a container image, scan it for vulnerabilities before storage, and deploy it to the cluster with no manual steps. Which approach BEST satisfies this requirement using Google Cloud native tooling?

A) Configure a Cloud Build trigger on the repository that builds the image, pushes it to Artifact Registry with vulnerability scanning enabled, then runs a deploy step against the GKE cluster
B) Install Jenkins on a Compute Engine VM and configure it to poll the repository every 5 minutes for changes
C) Use Cloud Scheduler to trigger a nightly Cloud Function that rebuilds and redeploys the application
D) Manually run 'gcloud builds submit' and 'kubectl apply' whenever a developer reports the branch has changed

---

**Q18.** A company has a Shared VPC hosting three projects: prod-app, prod-db, and analytics. The security team requires that VMs in the analytics project can only communicate with VMs in prod-db on TCP port 5432, and must be denied all other access to prod-db, regardless of future changes to broader firewall rules. Which approach BEST meets this requirement?

A) Create a hierarchical firewall policy attached to the folder containing prod-db that denies all ingress except TCP 5432 from the analytics subnet's service account, ensuring it evaluates before VPC-level rules
B) Create a single VPC firewall rule in the Shared VPC host project allowing TCP 5432 from the analytics subnet to the prod-db subnet, with a priority lower than existing allow rules
C) Use hierarchical firewall policies at the organization node to allow TCP 5432 between the two subnets
D) Configure VPC Service Controls around the prod-db project to restrict API access to only the analytics project

---

**Q19.** A financial services company runs workloads on GKE and needs those workloads to call Google Cloud APIs (e.g., Cloud Storage, BigQuery) without storing any downloadable service account keys in the cluster, due to a security audit requirement that prohibits long-lived credentials. Which approach BEST meets this requirement?

A) Enable Workload Identity Federation for GKE and bind the Kubernetes service account to a Google service account via IAM policy binding
B) Create a service account, generate a JSON key, and store it as a Kubernetes Secret mounted into the pods
C) Use the Compute Engine default service account attached to each GKE node with broad Editor role
D) Distribute the same service account key to all pods via a shared ConfigMap and rotate it every 90 days

---

**Q20.** A healthcare company must ensure that all new Cloud Storage buckets and Compute Engine resources created anywhere in its GCP organization are restricted to the us and europe-west multi-regions only, to satisfy data residency requirements. Which mechanism should the architect configure at the Organization node?

A) An Organization Policy constraint using constraints/gcp.resourceLocations set to allowed values for us and eu regions
B) A VPC Service Controls perimeter scoped to the us and europe-west regions
C) A Cloud Armor security policy that blocks requests originating from disallowed regions
D) IAM Conditions on every project's Owner role restricting resource creation by region

---

**Q21.** A company must encrypt data in BigQuery using keys they generate, control the rotation schedule of, and can disable to immediately revoke access to the data, while still relying on Google to manage the underlying key infrastructure. Which encryption approach satisfies this?

A) Google-managed encryption keys (default encryption)
B) Customer-supplied encryption keys (CSEK) uploaded per request
C) Customer-managed encryption keys (CMEK) via Cloud KMS
D) Client-side encryption performed before data is uploaded to BigQuery

---

**Q22.** A company stores sensitive data in BigQuery and Cloud Storage and is concerned about an insider with legitimate IAM permissions exfiltrating that data to a personal Google Cloud project outside the organization. Which control specifically addresses this data exfiltration risk?

A) Enforce IAM Conditions requiring MFA for all data access
B) Enable Cloud Audit Logs for Data Access on all relevant services
C) Apply an Organization Policy restricting service account key creation
D) Configure a VPC Service Controls perimeter around the projects containing BigQuery and Cloud Storage

---

**Q23.** An architect needs to store and rotate database connection passwords used by multiple Cloud Run services, with fine-grained IAM access control and versioning, and separately needs to scan customer support ticket text for accidental inclusion of credit card numbers before storing it. Which pair of services should be used, respectively?

A) Cloud KMS for password storage and Cloud DLP for credit card detection
B) Secret Manager for password storage and Cloud Armor for credit card detection
C) Cloud KMS for password storage and Cloud Armor for credit card detection
D) Secret Manager for password storage and Cloud DLP for credit card detection

---

**Q24.** A service account used by a batch data pipeline needs permission only to read objects from a single Cloud Storage bucket and write query results to a single BigQuery dataset. Following least privilege principles, which role assignment is BEST?

A) Grant the service account Storage Object Viewer on the specific bucket and BigQuery Data Editor on the specific dataset
B) Grant the service account the Editor primitive role on the project
C) Grant the service account Owner role scoped to the project's Storage and BigQuery APIs
D) Grant the service account Storage Admin and BigQuery Admin roles at the project level

---

**Q25.** A retail company stores sensitive customer PII in BigQuery datasets and Cloud Storage buckets within a dedicated 'sensitive-data' project. The security team is concerned that a compromised service account credential or a misconfigured IAM binding could allow data to be copied to a different, unauthorized GCP project outside the organization. Which control should the architect implement to prevent this specific type of data exfiltration?

A) Enable Private Google Access on all subnets in the sensitive-data project
B) Apply a Cloud Armor security policy to the project's load balancers
C) Configure a VPC Service Controls perimeter around the sensitive-data project's resources
D) Migrate the project to a Shared VPC host project to centralize network administration

---

**Q26.** A healthcare company must encrypt patient records stored in Cloud Storage using customer-managed encryption keys. Compliance requirements state that the encryption keys must physically reside in the same region as the data and must be rotated automatically every 365 days. Which configuration satisfies these requirements?

A) Create a global Cloud KMS key ring, set the key rotation period to 90 days, and enable CMEK on the Cloud Storage buckets
B) Encrypt the data using Google-managed encryption keys, which rotate automatically by default
C) Create a regional Cloud KMS key ring in the same region as the storage buckets, set the key rotation period to 365 days, and enable CMEK on the buckets using that key
D) Generate a Customer-Supplied Encryption Key (CSEK) and provide it with every Cloud Storage API request, rotating it manually once a year

---

**Q27.** A retail company suffers a major production outage caused by a bad deployment. Leadership wants to learn from the incident and prevent it from recurring without discouraging engineers from taking ownership of future releases. Which process should the cloud architect recommend?

A) Identify the individual engineer responsible and require additional training
B) Require VP-level manual sign-off for every future deployment
C) Disable the CI/CD pipeline until an investigation committee is formed
D) Conduct a blameless postmortem that documents root cause and actionable follow-up items

---

**Q28.** A company runs a steady-state production workload on Compute Engine 24/7 and is willing to commit to a 3-year usage term in exchange for the maximum possible discount on that predictable capacity. Which purchasing option should the architect recommend?

A) Sustained use discounts
B) Preemptible VMs / Spot VMs
C) Committed use discounts (CUDs)
D) Free Tier usage credits

---

**Q29.** A financial services company wants to add fraud detection to its application but has no in-house machine learning expertise and needs to minimize time to market. Which approach best fits a build-vs-buy decision in this context?

A) Build a custom TensorFlow model from scratch and train it on Compute Engine GPUs
B) Hire and ramp up a dedicated in-house ML engineering team over the next year
C) Deploy a self-managed Spark MLlib cluster on GKE
D) Use Vertex AI AutoML or a prebuilt fraud detection API

---

**Q30.** A team deploying to GKE wants to gradually shift a percentage of production traffic to a new application version and automatically roll back if error rates spike, as part of their managed CI/CD release process. Which Google Cloud configuration achieves this?

A) Configure a Cloud Build trigger that filters on the release branch name
B) Enable vulnerability scanning in Artifact Registry
C) Mirror the repository using Cloud Source Repositories
D) Define a canary deployment strategy in a Cloud Deploy delivery pipeline configuration

---

**Q31.** A product team consistently prioritizes new features over refactoring, resulting in growing technical debt that is starting to slow delivery velocity. Which practice best balances technical debt against ongoing feature delivery?

A) Address technical debt only after the entire feature backlog has been completed
B) Allocate a fixed percentage of each sprint or roadmap cycle to continuously address technical debt
C) Ignore technical debt unless it directly causes a production outage
D) Address technical debt only during a major annual version release

---

**Q32.** A company's current change management process requires full Change Advisory Board (CAB) review for every production change, causing release delays. Leadership wants faster, safer releases while still maintaining a compliance audit trail. Which approach should the architect recommend?

A) Require full Change Advisory Board (CAB) approval for every change, regardless of risk
B) Eliminate change tracking entirely to speed up releases
C) Implement CI/CD pipelines with policy-as-code checks (e.g., Binary Authorization) and rely on Cloud Audit Logs for traceability, removing manual approval for low-risk changes
D) Consolidate all releases into infrequent, large 'big-bang' quarterly deployments

---

**Q33.** A company's payment-processing service experienced a 45-minute outage last week. During the incident retrospective meeting, several engineers were reluctant to share details about the deployment that triggered the outage because a director from another team was present and known to reprimand individuals for mistakes. As cloud architect, which practice should you recommend to improve the effectiveness of post-incident reviews going forward?

A) Require the on-call engineer who caused the outage to write a personal action plan and present it to the director
B) Institute blameless postmortems that focus on identifying systemic and process failures rather than individual fault, with documented timelines and action items tracked to completion
C) Limit postmortem meetings to only the SRE team so that other stakeholders cannot ask uncomfortable questions
D) Replace postmortem meetings with an automated incident report generated solely from Cloud Monitoring alert logs

---

**Q34.** A retail company's mobile app team wants to reduce time-to-market for new features. Currently, every code change requires a manual QA sign-off that takes 3 days, and releases occur once per month. The team has strong software engineering skills but limited operations experience. Which change should you recommend first to best optimize this technical process?

A) Introduce automated testing (unit, integration) integrated into a CI/CD pipeline so manual QA is reduced to exception cases, enabling more frequent, smaller releases
B) Move release approval entirely to the business stakeholders so QA is no longer required before production release
C) Increase release frequency to twice per month while keeping the manual QA process unchanged
D) Outsource the QA function to a third-party vendor to keep the 3-day manual review but run it in parallel with development

---

**Q35.** A company needs to deploy identical Google Cloud infrastructure across separate dev, staging, and production projects. Leadership requires a full audit history of every infrastructure change and the ability to roll back to a previous known-good state quickly. Which approach BEST meets these requirements?

A) Use Cloud Shell to manually run gcloud commands in each project and record the steps in a shared document
B) Define the infrastructure as code using Terraform configurations stored in a version-controlled repository, applied through a CI/CD pipeline
C) Use the Cloud Console to click through resource creation in each project and export instance templates for reuse
D) Write a collection of bash scripts using gcloud commands and store them in a Cloud Storage bucket

---

**Q36.** A development team wants an automated pipeline that builds a container image whenever code is pushed to a Cloud Source Repositories repo, and then deploys the new image to GKE. Which Google Cloud service should orchestrate this build-and-deploy pipeline?

A) Cloud Scheduler
B) Cloud Composer
C) Cloud Build
D) Cloud Tasks

---

**Q37.** An architect needs a CI/CD pipeline running outside Google Cloud to authenticate and deploy resources on behalf of the organization, without relying on any individual's personal Google account credentials. Which approach should be used?

A) Have the pipeline run 'gcloud auth login' interactively each time it executes
B) Share the architect's personal OAuth refresh token with the pipeline configuration
C) Authenticate using a service account, ideally via workload identity federation or, if required, a service account key with gcloud auth activate-service-account
D) Store the project owner's Google account password as a pipeline secret

---

**Q38.** Which statement best describes the primary advantage of using Infrastructure as Code (IaC) tools such as Terraform or Deployment Manager over manual, console-based provisioning during implementation of a Google Cloud architecture?

A) IaC tools automatically scale compute resources up or down based on real-time traffic
B) IaC provides declarative, version-controlled, and repeatable deployments that can be reviewed and rolled back
C) IaC is the only supported method for creating resources in Google Cloud
D) IaC eliminates the need for a separate testing or staging environment

---

**Q39.** Before promoting a new application version from staging to production, the operations team wants to validate that it behaves correctly under production-like load while minimizing risk to real users. Which approach BEST achieves this during implementation?

A) Deploy the new version directly to 100% of production traffic and monitor Cloud Monitoring for error spikes
B) Perform a canary or blue/green deployment, routing a small percentage of production traffic to the new version while load-testing it before a full rollout
C) Rely on manual testing already completed in staging and skip further validation
D) Ask a subset of end users to report issues after the new version is fully released

---

**Q40.** A financial services company runs a critical workload on Cloud SQL for PostgreSQL. The business requires an RPO of 5 minutes and an RTO of 10 minutes in the event of a full regional outage. Which configuration BEST meets these requirements?

A) Enable Cloud SQL high availability (regional) configuration only
B) Create a cross-region read replica and implement automated procedures to promote it to a standalone primary during a regional outage
C) Configure automated daily backups with point-in-time recovery
D) Migrate the database to a single-region Cloud Spanner instance

---

**Q41.** A team runs services on App Engine and GKE and wants unhandled application exceptions to be automatically detected, deduplicated, and grouped by stack trace across all services, without writing custom log queries. Which Cloud Operations tool should they use?

A) Cloud Monitoring
B) Cloud Trace
C) Error Reporting
D) Cloud Profiler

---

**Q42.** A service has a defined SLO of 99.9% availability measured over a rolling 30-day window. Approximately how much total downtime does the associated error budget allow within that 30-day window?

A) 43.2 minutes
B) 4.32 minutes
C) 7.2 hours
D) 21.6 minutes

---

**Q43.** A team wants to release a new application version to production by routing a small percentage of live traffic to it while monitoring error rates and latency, with the ability to quickly shift traffic back to the previous version if problems appear, before rolling out to 100% of users. Which deployment strategy should they use?

A) Blue-green deployment
B) Rolling update
C) Canary deployment
D) Recreate deployment strategy

---

**Q44.** Which statement correctly distinguishes a Service Level Indicator (SLI) from a Service Level Objective (SLO)?

A) An SLI is defined by a legal contract, while an SLO is measured internally by the operations team
B) An SLA and an SLO are functionally identical and used interchangeably
C) An SLI is a quantitative measure of some aspect of a service's behavior, while an SLO is a target value or range of values for that SLI
D) An SLI is the target value for a metric, while an SLO is the actual measured value of that metric

---

**Q45.** A stateful application on GKE uses zonal persistent disks for storage. The company needs the ability to restore application data to a different region within one hour after a regional outage. Which approach BEST satisfies this requirement?

A) Configure regional persistent disks, which synchronously replicate data across two zones within the same region only
B) Rely on GKE's default automatic disk resizing feature
C) Use local SSDs for all persistent volumes to maximize IOPS
D) Create a snapshot schedule for the persistent disks with snapshots stored in a multi-region location, enabling restoration to a disk in a different region

---


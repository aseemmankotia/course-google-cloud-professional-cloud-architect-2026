## Chapter 7: Encryption, Data Protection & Network Security Controls — Practice Questions

**Q1.** A financial services company requires that Google never stores or has access to their disk encryption key material at rest, even inside Cloud KMS. The key must be supplied by the customer with every API call and exist only in memory during the operation. Which encryption approach meets this requirement?

A) Customer-supplied encryption keys (CSEK)
B) Customer-managed encryption keys (CMEK) with Cloud KMS
C) Default Google-managed encryption
D) Cloud HSM-backed CMEK keys

<details>
<summary>Answer</summary>

**Correct: A**

CSEK lets you supply your own AES-256 key on each request; Google uses it in memory to encrypt/decrypt and does not persist it, satisfying 'Google never stores the key' requirements.

**Why the others are wrong:**
- CMEK stores and manages the key inside Cloud KMS — Google's infrastructure holds the key material even though the customer controls IAM/rotation.
- Default encryption uses Google-owned and Google-managed keys with no customer control at all.
- Cloud HSM-backed CMEK still stores the key inside Google-managed KMS/HSM infrastructure, just with hardware protection.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A retail company runs BigQuery and Cloud Storage in multiple projects. Security wants to guarantee that even a compromised service account credential cannot be used to copy data to a storage bucket outside the organization's projects. Which control should they implement?

A) Cloud Armor security policy on the load balancer
B) Shared VPC with a central host project
C) VPC Service Controls perimeter around the projects
D) Cloud DLP inspection jobs on all buckets

<details>
<summary>Answer</summary>

**Correct: C**

VPC Service Controls create a service perimeter that blocks API-level data exfiltration to resources outside the perimeter, even with valid but compromised credentials.

**Why the others are wrong:**
- Cloud Armor protects HTTP(S) load balancers from web attacks and DDoS, not API-level exfiltration between projects.
- Shared VPC controls network connectivity/IP administration, not API data-exfiltration boundaries.
- Cloud DLP finds and redacts sensitive data but does not prevent exfiltration paths.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A public-facing web application behind a global external Application Load Balancer is being hit with SQL injection attempts and a volumetric DDoS attack. Which service should be configured on the load balancer's backend service to mitigate both?

A) Cloud IDS
B) Identity-Aware Proxy
C) Cloud Armor with preconfigured WAF rules
D) Cloud NAT

<details>
<summary>Answer</summary>

**Correct: C**

Cloud Armor attaches to the backend service of a global external HTTP(S) load balancer and provides both L3/L4/L7 DDoS protection and preconfigured WAF rules (OWASP ModSecurity CRS) including SQLi/XSS signatures.

**Why the others are wrong:**
- Cloud IDS detects network threats via packet mirroring; it doesn't block traffic at the load balancer.
- IAP controls user-level access to applications, not L7 attack signatures or DDoS.
- Cloud NAT provides outbound internet access for private instances, unrelated to inbound attack mitigation.

</details>

---

**Q4.** A healthcare company stores millions of scanned documents in Cloud Storage and must automatically identify and mask Social Security numbers before the files are shared with a third party. Which GCP service should be used?

A) Cloud DLP (Sensitive Data Protection)
B) Cloud KMS
C) Cloud Armor
D) Security Command Center

<details>
<summary>Answer</summary>

**Correct: A**

Cloud DLP (rebranded Sensitive Data Protection) uses built-in and custom infoTypes to inspect content and can redact, mask, or tokenize sensitive data like SSNs.

**Why the others are wrong:**
- Cloud KMS manages encryption keys, it doesn't inspect content for sensitive data patterns.
- Cloud Armor is a network/edge security service for load balancers, not content inspection.
- Security Command Center is a security posture/findings dashboard, not a data classification/redaction engine.

</details>

---

**Q5.** A development team currently hardcodes database passwords and third-party API keys directly in application source code deployed to Cloud Run. What is the recommended remediation?

A) Move secrets to Secret Manager and reference them via IAM-controlled access at runtime
B) Store secrets as environment variables in the container image build
C) Encrypt the source code repository with CMEK
D) Store secrets in a private Cloud Storage bucket with signed URLs

<details>
<summary>Answer</summary>

**Correct: A**

Secret Manager centralizes secret storage with versioning, audit logging, and fine-grained IAM, letting Cloud Run access secrets at runtime without embedding them in code or images.

**Why the others are wrong:**
- Baking secrets into the image still exposes them in image layers and build logs.
- Encrypting the repo protects the code at rest, not the exposure of plaintext secrets used at runtime.
- Using GCS with signed URLs adds unnecessary complexity and lacks the built-in versioning/IAM/audit model of Secret Manager.

</details>

---

**Q6.** A company operating in the EU must ensure a specific secret's data, including all replicas, never leaves EU regions due to data residency regulations. How should the secret be configured in Secret Manager?

A) User-managed replication policy restricted to EU regions
B) Automatic replication policy (Google chooses regions)
C) Store the secret in Cloud KMS instead of Secret Manager
D) Enable CMEK on the secret with a global key ring

<details>
<summary>Answer</summary>

**Correct: A**

Secret Manager's user-managed replication policy lets you explicitly pin secret replicas to specific regions, satisfying data residency requirements.

**Why the others are wrong:**
- Automatic replication lets Google choose storage locations globally, which can violate residency requirements.
- Cloud KMS stores encryption keys, not application secrets like passwords or tokens — it's the wrong service for this use case.
- CMEK on a secret controls the encryption key used, not the geographic location of the stored data.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A security team wants Cloud KMS to automatically generate new key versions for a CMEK key on a fixed schedule. What is the minimum rotation period Cloud KMS allows for automatic key rotation?

A) 1 hour
B) 7 days
C) 30 days
D) 24 hours

<details>
<summary>Answer</summary>

**Correct: D**

Cloud KMS requires a minimum automatic rotation period of 24 hours between key version rotations.

**Why the others are wrong:**
- 1 hour is shorter than the platform's supported minimum rotation interval.
- 7 days is a valid rotation interval but not the documented minimum allowed.
- 30 days is a common practical choice but is not the enforced minimum limit.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement correctly differentiates default Google-managed encryption from CMEK in Cloud Storage?

A) Google-managed encryption offers no encryption at rest, while CMEK does
B) CMEK requires the customer to supply the raw key bytes on every API request
C) With CMEK, the customer controls key rotation, IAM permissions, and can revoke/destroy the key to render data inaccessible; with Google-managed encryption, Google fully controls the key lifecycle
D) Google-managed encryption keys are stored in the customer's Cloud KMS key ring

<details>
<summary>Answer</summary>

**Correct: C**

Both approaches encrypt data at rest by default, but CMEK gives the customer control over key lifecycle (rotation, IAM, destruction) via Cloud KMS, while Google-managed keys are fully controlled and rotated by Google.

**Why the others are wrong:**
- Google-managed encryption is still full encryption at rest — GCP encrypts all data by default regardless of key type.
- Supplying raw key bytes per request describes CSEK, not CMEK.
- Google-managed keys are stored in Google's internal key management, not the customer's KMS key ring — that's the defining difference from CMEK.

</details>

---


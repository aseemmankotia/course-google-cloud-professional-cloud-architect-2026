# Chapter 7 Cheat Sheet: Encryption, Data Protection & Network Security

## Encryption Key Models
| Model | Who holds key | Use case | Notes |
|---|---|---|---|
| Google-managed | Google | Default, no config needed | Always-on, no customer key control |
| CMEK | Customer, via Cloud KMS | Need rotation/IAM/audit/destroy control | Key stored in Google infra (KMS/HSM) |
| CSEK | Customer, supplied per-request | Regulatory requirement that Google never stores key | AES-256, base64; only Compute Engine disks/images & Cloud Storage support it |

**Exam trap:** CSEK requires supplying the key on *every* API call — if the exam says "Google must never persist the key at rest," the answer is CSEK, not CMEK.

## Cloud KMS Key Facts
- Automatic rotation minimum period: **24 hours**
- Destroying a key version (CMEK) makes CMEK-encrypted data permanently unrecoverable — used as an org-level "crypto-shred" data deletion strategy.

## VPC Service Controls
- Creates a **service perimeter** around projects to stop **data exfiltration** (even from compromised credentials or malicious insiders).
- Protects specified **APIs** of supported services (GCS, BigQuery, BigTable, etc.), not general network traffic.
- **Access Levels** (via Access Context Manager) define conditional exceptions based on IP, device trust, identity.
- Different from Shared VPC (network/IP admin) and IAM (permission grants) — VPC SC is a perimeter boundary layer on top of both.

## Cloud Armor
- Attaches to backend service of **global external Application Load Balancer**.
- Provides: L3/L4/L7 **DDoS protection** + **WAF** via preconfigured rules (OWASP ModSecurity CRS: SQLi, XSS, RCE, etc.) + custom rules + rate limiting.
- Tiers: Standard (always-on basic protections) vs Managed Protection Plus/Enterprise (adds Adaptive Protection ML-based detection, named IP threat intel).
- **Exam trap:** Cloud Armor only protects HTTP(S) LB-fronted resources, not arbitrary VMs or internal traffic.

## Cloud DLP (Sensitive Data Protection)
- Detects sensitive data via **infoTypes** (150+ built-in: SSN, credit card, email, etc.) plus custom regex/dictionary infoTypes.
- Actions: **redact, mask, tokenize (format-preserving encryption), bucketize, k-anonymity/l-diversity risk analysis**.
- Use for scanning Cloud Storage, BigQuery, Datastore, or streaming content before sharing/export.

## Secret Manager
- Centralized secret storage — replaces hardcoding secrets in code/images.
- Max secret **payload: 64 KiB** per version.
- Replication: **Automatic** (Google picks regions) vs **User-managed** (pin regions — needed for data residency).
- IAM at secret level + full version history + audit logging via Cloud Audit Logs.

## Data Residency / Compliance
- Enforced via **Organization Policy** (resource location constraints) + service-level region pinning (e.g., Secret Manager user-managed replication, GCS bucket location, BigQuery dataset location).
- Case-study signal words: "data must not leave region X," "regulator requires key destruction capability," "third-party must never see raw PII" → map to CMEK/CSEK, DLP, and residency org policies respectively.

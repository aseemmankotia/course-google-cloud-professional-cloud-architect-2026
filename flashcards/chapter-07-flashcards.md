## Chapter 7: Encryption, Data Protection & Network Security Controls — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | CMEK vs CSEK: who stores the key material? | CMEK: key lives in Cloud KMS (Google's infrastructure), customer controls IAM/rotation/destroy. CSEK: customer supplies raw AES-256 key on every request; Google never persists it. Exam tip: CSEK = 'bring key each call', CMEK = 'manage key in KMS'. |
| 2 | CSEK key format requirement? | 256-bit AES key, base64-encoded, supplied by the customer on each request to supported services (Compute Engine disks/images, Cloud Storage). |
| 3 | Secret Manager maximum payload size per secret version? | 64 KiB (65,536 bytes). Exam tip: for larger blobs, store in Cloud Storage/KMS-encrypted objects and keep only a reference/small secret in Secret Manager. |
| 4 | Cloud KMS minimum automatic rotation period? | 24 hours between rotations. Exam tip: shorter than 24h is not supported for automatic rotation. |
| 5 | Primary purpose of VPC Service Controls? | Creates a service perimeter around projects/resources to prevent data exfiltration via APIs — blocks access to protected services (e.g., GCS, BigQuery) from outside the perimeter even with valid credentials. |
| 6 | When to use Cloud Armor vs Cloud DLP? | Cloud Armor = network/edge protection (DDoS + WAF) for global external HTTP(S) load balancers. Cloud DLP = content inspection/classification/redaction of sensitive data (PII, SSNs, credit cards). Different layers of the stack — don't confuse them. |
| 7 | What ruleset do Cloud Armor's preconfigured WAF rules use? | OWASP ModSecurity Core Rule Set (CRS) — covers SQLi, XSS, LFI/RFI, and other common web attack signatures. |
| 8 | What is a Cloud DLP 'infoType'? | A detector/classifier for a category of sensitive data (e.g., US_SOCIAL_SECURITY_NUMBER, CREDIT_CARD_NUMBER). GCP provides 150+ built-in infoTypes; custom infoTypes can be defined via regex or dictionaries. |
| 9 | Secret Manager replication policy types? | Automatic (Google chooses regions, simplest, no residency guarantee) vs User-managed (pin replicas to specific regions — required for data residency compliance). |
| 10 | How is data residency typically enforced at the org level in GCP? | Organization Policy constraints (e.g., resource locations constraint) restrict which regions resources can be created in, complementing service-level controls like Secret Manager's user-managed replication. |
| 11 | Default encryption at rest in GCP — who manages the key? | Google-managed encryption keys are used by default on all data at rest; Google fully controls generation, rotation, and storage — no customer configuration or IAM control over the key itself. |
| 12 | What defines a VPC Service Controls 'access level'? | Configured via Access Context Manager based on attributes like source IP range, device policy, or identity — allows conditional access into/out of a service perimeter (e.g., allow corp network but block public internet). |

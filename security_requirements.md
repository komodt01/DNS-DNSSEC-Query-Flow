# Security Requirements

## 1. Integrity and Authenticity

1.1 The guide must explain that DNSSEC provides data integrity and origin authentication using:
- DNSKEY records (zone public keys)
- RRSIG records (signatures over RRsets)
- DS records (delegation signer records in parent zones)

1.2 The documentation must clearly differentiate between:
- Unsigned zones (no DNSSEC protection)
- Signed zones that validate successfully (secure)
- Signed zones that fail validation (bogus)

1.3 The diagram and text must show where the recursive resolver:
- Retrieves DNSKEY and DS records
- Validates signatures using the trust anchor (typically the root key)

## 2. Trust Model

2.1 The project must describe the DNSSEC chain of trust:
- Root zone → TLD → Second-level zone

2.2 The guide must state that:
- Compromise of a parent zone’s keys can impact all delegated children.
- Trust anchors must be securely managed (e.g., root KSK).

2.3 The text must highlight the difference between:
- Validating resolvers (perform DNSSEC checks)
- Non-validating resolvers (forward responses without verification)

## 3. Resolver and Cache Behavior

3.1 The guide must show that the recursive resolver:
- Caches both DNS answers and DNSSEC metadata (RRSIG, DNSKEY).
- Respects TTLs to avoid serving stale or expired data.

3.2 The documentation must explain the security impact of:
- Serving expired signatures (validation failure).
- Misconfigured TTLs or improper negative caching.

3.3 The resolver’s behavior on failure must be defined:
- Validation failure should result in SERVFAIL or equivalent.
- The client must not receive unauthenticated data as “secure”.

## 4. Key Management Considerations

4.1 The guide must mention that operational DNSSEC deployments require:
- Separate KSK (Key Signing Key) and ZSK (Zone Signing Key) roles.
- Regular key rotation and rollover procedures.

4.2 The risks of poor key management must be highlighted:
- Using overly long key lifetimes.
- Failing to perform coordinated DS updates in parent zones.

4.3 The project must clarify that private keys must never be stored in:
- Public repositories
- Shared file systems without adequate protection

## 5. Logging and Monitoring

5.1 The documentation must recommend monitoring for:
- DNSSEC validation failures
- Sudden spikes in SERVFAIL responses
- Unexpected changes in DNSKEY or DS records

5.2 For cloud environments, the guide should reference:
- Route 53 DNS query logs (AWS)
- Cloud DNS logging (GCP)
- Azure DNS logs

5.3 Logs must be described as important inputs for:
- Incident response
- Forensics after suspected poisoning or hijacking attempts

## 6. Client and Application Behavior

6.1 The guide must explain that many clients rely on:
- Recursive resolvers operated by ISPs, enterprises, or cloud providers.

6.2 It should encourage validating resolvers or DNSSEC-aware services for:
- Sensitive applications
- High-risk domains (financial, healthcare, government)

6.3 The documentation must clarify that:
- Applications should not assume “DNS is secure” unless:
  - DNSSEC validation is enforced
  - Resolver behavior is trusted and monitored

## 7. Cloud and Hybrid Considerations

7.1 The project must call out how these principles apply when:
- Using cloud-managed DNS zones (Route 53, Azure DNS, Cloud DNS).
- Integrating on-prem resolvers with cloud DNS.

7.2 The guide should highlight:
- Where DNSSEC signing occurs (authoritative side).
- Where validation normally occurs (recursive side).

7.3 Any example architectures must avoid implying:
- That DNSSEC alone is sufficient; additional controls (firewalls, WAF, IAM) are still required.

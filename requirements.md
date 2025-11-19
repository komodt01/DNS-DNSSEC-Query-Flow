# Requirements

## Functional Requirements

1. The guide must describe the full DNS resolution path:
   - Client stub resolver
   - Recursive resolver
   - Cache behavior
   - Root, TLD, and authoritative name servers
   - Final answer returned to the client

2. The guide must explain how DNSSEC works at a high level:
   - Signed zones (RRSIG, DNSKEY, DS records)
   - Chain of trust from root to zone
   - Validation outcome (secure, insecure, bogus)

3. The documentation must show where caching occurs and how TTL affects:
   - When records are reused from cache
   - When new lookups are triggered

4. The project must include a diagram that visually represents:
   - The DNS query path
   - Where DNSSEC validation happens
   - Where failures can occur

5. The repository must include separate files for:
   - Design overview (`design_overview.md`)
   - Security requirements (`security_requirements.md`)
   - Risks and mitigations (`risks_and_mitigations.md`)
   - README (`README.md`)

## Non-Functional Requirements

1. **Clarity**  
   Explanations must be written in plain language suitable for:
   - Security architects
   - Cloud engineers
   - Students learning DNS and DNSSEC

2. **Consistency**  
   Terminology must be consistent across files:
   - “Recursive resolver” vs “caching resolver”
   - “Authoritative server” vs “authoritative name server”
   - “Validation failure” vs “bogus response”

3. **Portability**  
   The concepts must apply across major cloud providers:
   - AWS Route 53
   - Azure DNS
   - Google Cloud DNS

4. **Security Emphasis**  
   The focus must stay on:
   - How DNSSEC mitigates spoofing and cache poisoning
   - Where trust anchors and keys matter
   - What happens when validation fails

5. **No Credentials or Secrets**  
   The repo must not contain:
   - Real domain names used in production
   - Private keys, KSK, or ZSK material
   - API keys or cloud account identifiers

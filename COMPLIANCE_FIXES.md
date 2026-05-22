# Compliance Studio — audit 18eceb9f

_Generated 2026-05-22T13:16:58.469Z_

Posture score: **0/100**

1 findings included in this PR.

---

## 1. Granular, Unbundled and Revocable Consent
- **Severity**: critical
- **Framework**: DPDPA
- **Location**: `Project Codebase`
The DPDPA mandates granular, unbundled, and easily revocable consent for data processing. Given the complete absence of evidence demonstrating compliance with this rule, and specific signals indicating missing code call sites and documentation, it is highly probable that the current consent mechanisms do not meet the stringent requirements of the DPDPA. This is a fundamental requirement for any data fiduciary operating under DPDPA, especially for a healthtech AI company handling sensitive personal data. The lack of evidence is a strong indicator of non-compliance. (Evidence missing: Missing code call site with tag ${req.tag}, URL or Doc signal '${req.field}' does not match expected ${req.expected})

**Fix:** Implement a robust consent management platform (CMP) or equivalent system that ensures consent is free, specific, informed, unconditional, and unambiguous. Explicitly unbundle consent for data processing from core terms of service. Ensure that data principals can withdraw consent as easily as they granted it, with clear mechanisms for doing so. All consent flows and withdrawal processes must be thoroughly documented and auditable, with relevant code call sites tagged and URL/Doc signals updated to reflect compliance.

```
// Check user consent before initiating third-party API or AI generation
import { brane } from '@brane-sdk/node';

const consent = await brane.checkConsent({
  userId: user.id,
  purpose: 'ai_diagnosis',
  dataCategory: 'clinical_notes'
});

if (!consent.allowed) {
  throw new Error("Consent not granted or revoked for purpose: ai_diagnosis");
}
```


---

## Reference Implementations

The companion file `compliance.policies.json` is the runtime manifest the Compliance Studio SDK loads at startup.
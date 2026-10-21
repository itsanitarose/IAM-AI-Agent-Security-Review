# 03 — Identity Governance Findings

**Project:** Northwind Health | AI Agent Security Review  
**Identity:** `svc-supportbot`

---

## 1. Governance Review Overview

This assessment examines how SupportBot's non-human identity is owned, managed and reviewed.

SupportBot was created 14 months ago by a contractor who has since left the organisation. Its identity has no assigned owner, its API token has never been rotated, and the same credential is used in production and staging.

The objective is to identify governance weaknesses that could allow unauthorised or unnecessary access to remain undetected.

## 2. Governance Findings and Risk Register

| ID | Finding | Severity | Recommended Action |
|---|---|---|---|
| G-01 | No accountable identity owner | High | Assign a business owner and technical owner with defined responsibilities. |
| G-02 | Non-expiring, unrotated API token | High | Coordinate secure credential replacement and revocation, verify invalidation of the old token, and establish expiry and rotation requirements. |
| G-03 | Shared credential across environments | High | Separate production and staging identities and credentials. |
| G-04 | No periodic identity and access review | High | Establish scheduled reviews of the identity, its permissions and continued business need. |

*Severity ratings are qualitative assessments based on the supplied scenario.*

## 3. Detailed Governance Findings

### G-01 — No Accountable Identity Owner

**Severity: High**

SupportBot's owner field is blank, and the contractor who created the identity has left the organisation.

There is no named person accountable for reviewing its continued business need, managing its credentials or ensuring that the identity is securely maintained or retired.

**Risk:** Without clear ownership, security weaknesses may remain unresolved and unnecessary access may continue without appropriate oversight.

**Recommendation:** Assign a business owner and technical owner, document their responsibilities and ensure ownership is updated when personnel or business requirements change.

### G-02 — Non-Expiring, Unrotated API Token

**Severity: High**

SupportBot's API token has no expiry date and has never been rotated in 14 months.

If the credential is stolen or exposed, it could remain usable until explicitly revoked, potentially allowing prolonged unauthorised access.

**Risk:** A long-lived credential increases the potential impact of credential exposure or misuse.

**Recommendation:** Coordinate the secure replacement and revocation of the existing token, verify that the old credential can no longer authenticate, and establish appropriate expiry, rotation and secure storage requirements.

### G-03 — Shared Credential Across Environments

**Severity: High**

SupportBot uses the same API token in production and staging.

If the credential is exposed in staging, it could also be used to access production resources, depending on the permissions and systems associated with the token.

**Risk:** Shared credentials weaken environment separation and increase the potential impact of a compromise.

**Recommendation:** Use separate identities and credentials for production and staging, with permissions limited to the requirements of each environment.

### G-04 — No Periodic Identity and Access Review

**Severity: High**

SupportBot's identity and access have not been reviewed since launch.

Without regular reviews, there is no assurance that its access remains appropriate, its credentials are securely managed or its continued business need has been confirmed.

**Risk:** Unnecessary permissions and outdated identity configurations may remain in place without detection.

**Recommendation:** Introduce quarterly identity and access reviews, with additional reviews following significant changes to the agent's responsibilities, configuration or ownership.

## 4. Governance Risk Summary

All four findings are rated **High** because they affect the ongoing security and accountability of SupportBot's identity.

The combination of missing ownership, weak credential lifecycle management, shared credentials and absent periodic reviews creates conditions in which unauthorised access could persist without adequate oversight.

These weaknesses should be addressed through accountable ownership, controlled credential management, environment separation and regular identity reviews.

## 5. Assessment Outcome

The review identifies four governance weaknesses requiring remediation.

The recommended actions establish clearer accountability and stronger lifecycle controls for SupportBot's non-human identity.

These findings and recommendations are based on the supplied scenario. No identity configurations or credentials were changed as part of this assessment.

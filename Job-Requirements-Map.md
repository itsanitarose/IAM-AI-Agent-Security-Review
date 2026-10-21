# Job Requirements Map

**Project:** Northwind Health | AI Agent Security Review  
**Focus Area:** Identity and Access Management (IAM) | Non-Human Identity Security

---

## 1. Project Overview

The Northwind Health AI Agent Security Review evaluates the identity, permissions, credential security and operational activity of SupportBot, an AI-powered support agent.

The engagement addresses excessive access privileges, identity governance weaknesses, credential lifecycle risks and suspicious patient-record activity.

The security approach combines access assessment, risk evaluation, incident-response recommendations and control design to establish an appropriate operating model for the non-human identity.

## 2. IAM Responsibilities and Project Evidence

| IAM Responsibility | Project Application | Supporting Evidence |
|---|---|---|
| Access review and certification | Assessed nine permissions against SupportBot's authorised business functions and determined required, conditional and unnecessary access. | [02 — Permission Review](documents/02-Permission-Review.md) |
| Least-privilege access control | Defined a restricted permission model for support information, billing summaries and ticket-management operations. | [02 — Permission Review](documents/02-Permission-Review.md) |
| Identity governance | Identified ownership gaps, missing access reviews and weaknesses in non-human identity accountability. | [03 — Identity Governance Findings](documents/03-Identity-Governance-Findings.md) |
| Credential lifecycle security | Evaluated non-expiring API credentials, rotation requirements, revocation procedures and production/staging credential separation. | [03 — Identity Governance Findings](documents/03-Identity-Governance-Findings.md) |
| Security risk assessment | Evaluated governance weaknesses and suspicious access activity, including severity, potential impact and required follow-up. | [03 — Identity Governance Findings](documents/03-Identity-Governance-Findings.md) and [04 — Suspicious Activity Assessment](documents/04-Suspicious-Activity-Assessment.md) |
| Security event analysis | Analysed seven-day activity records and identified concentrated access to 1,900 patient records from an unfamiliar source IP. | [04 — Suspicious Activity Assessment](documents/04-Suspicious-Activity-Assessment.md) |
| Incident-response coordination | Defined escalation, credential containment, evidence preservation and IAM investigation-support procedures. | [04 — Suspicious Activity Assessment](documents/04-Suspicious-Activity-Assessment.md) |
| Security control design | Developed five controls addressing credential security, identity governance, least privilege, monitoring and separation of duties. | [05 — Recommended Security Controls](documents/05-Recommended-Security-Controls.md) |
| Security monitoring requirements | Defined authentication and API monitoring requirements, including alerts for unusual access patterns and sensitive actions. | [05 — Recommended Security Controls](documents/05-Recommended-Security-Controls.md) |
| Risk remediation planning | Established recommended actions and implementation priorities based on identified security concerns and operational dependencies. | [05 — Recommended Security Controls](documents/05-Recommended-Security-Controls.md) |

## 3. Technical Competencies

### Identity and Access Security

- Non-human identity and service account security.
- Permission inventory and access review.
- Least-privilege access design.
- Authorisation boundaries and restricted access workflows.
- Sensitive data access assessment.

### Identity Governance and Credential Management

- Identity ownership and accountability.
- Credential lifecycle management.
- API token expiry, rotation and revocation.
- Production and staging environment separation.
- Periodic and event-triggered access reviews.

### Security Operations and Risk Assessment

- Identity activity analysis.
- Authentication and API monitoring requirements.
- Suspicious access identification and risk classification.
- Incident escalation and containment planning.
- Evidence preservation and investigation support.

### Security Architecture and Control Design

- Identity security control design.
- Separation of duties.
- Human authorisation and approval workflows.
- Sensitive transaction restrictions.
- Risk-based remediation prioritisation.

## 4. Business and Security Alignment

| Business Requirement | IAM Security Approach |
|---|---|
| Maintain support operations | Preserve approved help-centre access and restricted ticket-management capabilities. |
| Protect patient information | Remove unrestricted patient-record access and enforce appropriate authorisation boundaries. |
| Protect financial transactions | Restrict payment-data access and require authorised Finance personnel to approve and execute refunds. |
| Maintain accountable communications | Require human review, approval and sending of outgoing support messages. |
| Establish identity accountability | Assign business and technical owners and introduce periodic access reviews. |
| Improve security visibility | Monitor authentication, API requests and unusual activity patterns. |
| Support operational resilience | Coordinate credential replacement, containment and access changes with responsible service owners. |

## 5. Security Deliverables

| Deliverable | Description |
|---|---|
| [01 — Scenario and Scope](documents/01-Scenario-and-Scope.md) | Business context, identity scope, security objectives and assessment approach. |
| [02 — Permission Review](documents/02-Permission-Review.md) | Permission inventory, access decisions and proposed least-privilege model. |
| [03 — Identity Governance Findings](documents/03-Identity-Governance-Findings.md) | Governance risk register, identity ownership findings and credential security recommendations. |
| [04 — Suspicious Activity Assessment](documents/04-Suspicious-Activity-Assessment.md) | Activity evidence, preliminary security risk assessment and recommended IAM incident response. |
| [05 — Recommended Security Controls](documents/05-Recommended-Security-Controls.md) | Target security controls, authorisation requirements and implementation priorities. |

## 6. Project Outcome

The security review identified excessive permissions, inadequate credential lifecycle controls, missing identity accountability and suspicious patient-record activity requiring investigation.

The resulting security recommendations establish a target operating model based on five control areas:

1. Credential security and environment separation.
2. Identity ownership and access reviews.
3. Least-privilege access.
4. Activity monitoring and alerting.
5. Separation of duties and human approval.

**Security Objective:** Establish a controlled, accountable and auditable non-human identity that supports authorised business operations while reducing exposure to sensitive information and preventing independent execution of high-risk actions.

# 05 — Recommended Security Controls

**Project:** Northwind Health | AI Agent Security Review  
**Identity:** `svc-supportbot`

---

## 1. Security Controls Overview

This assessment recommends security controls to reduce the risks identified in SupportBot's permission review, identity governance assessment and suspicious activity analysis.

SupportBot requires access to approved support information and limited ticket-management functions. However, its current identity configuration includes excessive permissions, weak credential management and insufficient oversight of sensitive actions.

The objective is to propose a more secure operating model based on least privilege, accountable identity ownership, credential security, monitoring and separation of duties.

## 2. Recommended Security Controls

| ID | Control Area | Recommended Control | Risk Addressed |
|---|---|---|---|
| C-01 | Credential security and environment separation | Use separate production and staging identities and credentials, with secure storage, expiry, rotation and revocation procedures. | Long-lived credentials and shared access across environments |
| C-02 | Identity ownership and access reviews | Assign accountable business and technical owners, with quarterly and change-triggered identity and access reviews. | Missing ownership and unreviewed access |
| C-03 | Least-privilege access | Remove unnecessary permissions and restrict retained access to approved support workflows. | Excessive access to patient, financial and support data |
| C-04 | Activity monitoring and alerting | Monitor authentication and API activity, with alerts for unusual access patterns and sensitive actions. | Potential credential misuse or unauthorised activity going undetected |
| C-05 | Separation of duties and human approval | Require authorised employees to approve and execute sensitive financial, patient-data and communication actions. | Unauthorised changes, refunds and outgoing communications |

## 3. Proposed Control Design

### C-01 — Credential Security and Environment Separation

SupportBot should use separate identities and credentials for production and staging.

Recommended measures include:

- Replace the existing shared API token through a controlled process.
- Store credentials securely rather than exposing them in application code or configuration files.
- Apply appropriate credential expiry and rotation requirements.
- Establish a documented process for revoking compromised or unnecessary credentials.
- Verify that replaced or revoked credentials can no longer authenticate.

**Expected Outcome:** Reduce the risk of prolonged credential misuse and prevent a credential exposed in one environment from automatically providing access to another.

### C-02 — Identity Ownership and Access Reviews

SupportBot should have clearly assigned business and technical owners responsible for its ongoing management.

Recommended measures include:

- Assign and document accountable identity owners.
- Define responsibility for credential management, access approval and identity retirement.
- Review the identity's business purpose and assigned permissions quarterly.
- Trigger additional reviews following changes to ownership, functionality or access requirements.
- Record review decisions and required remediation actions.

**Expected Outcome:** Establish accountability and ensure that SupportBot's identity and access remain appropriate throughout its lifecycle.

### C-03 — Least-Privilege Access

SupportBot should retain only the permissions required to perform its approved support responsibilities.

Recommended measures include:

- Retain access to approved help-centre articles.
- Restrict billing-summary access to relevant information for authenticated and authorised clinic staff.
- Allow support-ticket creation and limited updates within defined workflows.
- Remove unrestricted access to full patient records and payment data.
- Remove permissions to change patient contact details, issue refunds, send emails independently or delete ticket history.

**Expected Outcome:** Reduce unnecessary exposure to sensitive information and limit the actions available if SupportBot's identity is misused.

The detailed permission decisions are documented in [02 — Permission Review](02-Permission-Review.md).

### C-04 — Activity Monitoring and Alerting

SupportBot's authentication and API activity should be logged and monitored for unusual behaviour.

Recommended measures include:

- Record authentication attempts, API requests and sensitive actions.
- Alert on unusually high patient-record access volumes or concentrated access within short periods.
- Alert on access from unfamiliar source IP addresses, unusual activity patterns and unexpected sensitive actions.
- Monitor unexpected financial transactions, patient-data changes and outgoing communications.
- Retain relevant logs according to organisational security and investigation requirements.

**Expected Outcome:** Improve the ability to identify suspicious activity promptly and provide evidence for incident investigation.

The suspicious access event and initial IAM response are documented in [04 — Suspicious Activity Assessment](04-Suspicious-Activity-Assessment.md).

### C-05 — Separation of Duties and Human Approval

SupportBot should assist with support workflows without independently approving or executing sensitive actions.

Recommended measures include:

- Allow SupportBot to gather information and prepare support tickets within approved workflows.
- Route patient-contact changes to authorised employees for verification, approval and execution.
- Require authorised Finance personnel to review, approve and execute refunds.
- Require authorised employees to review, approve and send outgoing support communications.
- Record who approved and executed sensitive actions, together with the relevant timestamps.

**Expected Outcome:** Maintain human accountability for financial transactions, changes to patient information and external communications.

## 4. Should SupportBot Approve Refunds?

**Recommendation: No.**

SupportBot should not independently approve or issue refunds, including transactions below the existing $500 threshold.

Refund requests may involve misunderstood customer instructions, incorrect billing information or circumstances requiring human judgement.

SupportBot may help collect the relevant information, create a support ticket and prepare a recommendation. However, an authorised Finance employee should review the request, make the approval decision and execute the transaction.

This separation of duties reduces the risk of incorrect or unauthorised refunds and ensures that financial decisions remain attributable to an accountable employee.

## 5. Recommended Implementation Priorities

| Priority | Recommended Action | Reason |
|---|---|---|
| Immediate | Coordinate incident investigation and containment of the potentially compromised credential. | Address the suspicious patient-record access event. |
| High | Replace the shared credential and separate production and staging access. | Reduce the risk of continued credential misuse and cross-environment exposure. |
| High | Remove excessive permissions and restrict sensitive actions. | Limit unnecessary access to patient and financial information. |
| High | Assign accountable owners and establish human approval requirements. | Improve governance and accountability. |
| Ongoing | Introduce periodic access reviews, monitoring and alerting. | Support continued oversight and detection of unusual activity. |

Implementation should be coordinated with the relevant security, IAM, application and business owners to manage operational dependencies and service continuity.

## 6. Assessment Outcome

The proposed controls address five areas of risk: credential security, identity governance, excessive permissions, suspicious activity monitoring and insufficient human oversight of sensitive actions.

Together, these recommendations would allow SupportBot to continue supporting clinic staff while reducing unnecessary access and improving accountability.

**Conclusion:** SupportBot should operate as a restricted support assistant, not as an autonomous authority for financial transactions, patient-data changes or outgoing communications.


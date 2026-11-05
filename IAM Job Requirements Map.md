# IAM Skills Map

**Northwind Health | IAM: AI Agent Security Review**

This map connects the IAM job requirements I'm researching to the skills demonstrated in my SupportBot case study.

| Job Requirement | Evidence in This Project |
|:----------------|:-------------------------|
| **Access Reviews and Audits** | [02. Permission Review](documents/02.%20Permission%20Review.md): Reviewed SupportBot's nine permissions against its documented responsibilities and identified which access should be kept, restricted or removed. |
| **Least Privilege and Access Control** | [02. Permission Review](documents/02.%20Permission%20Review.md): Identified excessive access to patient information, billing data and sensitive actions. Proposed restrictions based on SupportBot's actual duties. |
| **Non-Human Identity Management** | [03. Identity Governance Findings](documents/03.%20Identity%20Governance%20Findings.md): Investigated the service account's missing owner, lack of access reviews, non-expiring token and shared credentials across environments. |
| **Identity Ownership and Lifecycle Governance** | [03. Identity Governance Findings](documents/03.%20Identity%20Governance%20Findings.md) · [05. Security Controls & Target State](documents/05.%20Security%20Controls%20%26%20Target%20State.md): Identified governance gaps and recommended named ownership, identity review dates and quarterly access reviews. |
| **Investigating Access Discrepancies** | [04. Suspicious Activity & Incident Response](documents/04.%20Suspicious%20Activity%20%26%20Incident%20Response.md): Examined unusual access to 1,900 patient records from an unfamiliar IP address and distinguished a suspected compromise from a confirmed breach. |
| **IAM Risk Assessment** | [03. Identity Governance Findings](documents/03.%20Identity%20Governance%20Findings.md): Documented six governance findings, assigned qualitative severity ratings and explained how the risks could affect patient information and financial actions. |
| **Credential and Access Remediation** | [05. Security Controls & Target State](documents/05.%20Security%20Controls%20%26%20Target%20State.md): Recommended token revocation, separate production and staging identities, secure credential storage and reduced permissions. |
| **IAM Troubleshooting and Verification Planning** | [05. Security Controls & Target State](documents/05.%20Security%20Controls%20%26%20Target%20State.md): Defined checks for authorised and denied access, credential expiry, environment separation and logging. These were proposed tests, not tests performed in a live system. |
| **Incident Escalation and Stakeholder Collaboration** | [04. Suspicious Activity & Incident Response](documents/04.%20Suspicious%20Activity%20%26%20Incident%20Response.md): Outlined how I would coordinate containment with IT and incident response, request evidence preservation and escalate possible patient-data exposure. |
| **Audit Evidence and Documentation** | [01. Source Data](documents/01.%20Source%20Data.md) · [03. Identity Governance Findings](documents/03.%20Identity%20Governance%20Findings.md): Organised identity and activity records and documented findings with supporting evidence and risk ratings. |
| **Machine Identity and AI Agent Security** | [02. Permission Review](documents/02.%20Permission%20Review.md) · [05. Security Controls & Target State](documents/05.%20Security%20Controls%20%26%20Target%20State.md): Assessed an AI agent's service identity, API permissions and credential risks, then proposed independently enforced authorisation and monitoring. |
| **Security Accountability and Human Oversight** | [06. Digging Deeper](documents/06.%20Digging%20Deeper.md): Examined who remains accountable for automated refund decisions and the need for human oversight, decision records, sampling and corrective action. |
<br>

## 🔍 Areas of Interest

- **Non-Human Identity Management:** Service accounts, ownership and credential management.
- **AI Agent Security:** Agent identities, permissions and access controls.

---

[Back to Project Overview](https://github.com/itsanitarose)


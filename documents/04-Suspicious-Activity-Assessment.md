# 04 — Suspicious Activity Assessment

**Project:** Northwind Health | AI Agent Security Review  
**Identity:** `svc-supportbot`

---

## 1. Suspicious Activity Overview

This assessment examines SupportBot's reported activity over seven days, with particular attention to unusual patient-record access associated with its non-human identity.

SupportBot is intended to answer clinic staff questions about appointment and billing status, create support tickets and draft responses for human approval.

An activity log identified a short period of concentrated patient-record access from an unfamiliar IP address.

The objective is to assess the security concern and recommend an appropriate initial IAM response without assuming that a breach has occurred.

The assessment is based on the supplied scenario and activity records. No live logs or systems were accessed.

## 2. Activity Evidence

### Seven-Day Activity Summary

| Activity | Recorded Volume | Observation |
|---|---|---|
| Patient records read | 38,400 | Within the stated normal weekly range of 35,000–45,000 |
| Patient contact details updated | 3 | Data-changing activity outside SupportBot's intended responsibilities |
| Refunds issued | 2 | $120 and $310, with no human approval recorded |
| Emails sent as support address | 612 | Direct email activity requiring verification of human approval |
| Support tickets created or updated | 1,150 | Consistent with an intended function, although individual actions were not validated |
| Ticket-history deletions | 0 | No deletions recorded |

Although the weekly patient-record access volume was within the stated normal range, this does not establish that every individual access event was authorised.

The contact-detail updates, refunds and outgoing emails also require review because SupportBot's intended role does not include independently performing these actions.

### Suspicious Access Event

| Attribute | Recorded Activity |
|---|---|
| Identity | `svc-supportbot` |
| Day | Tuesday |
| Time | 03:12–03:16 |
| Duration | 4 minutes |
| Patient records accessed | **1,900** |
| Source IP | `198.51.100.77` |
| Usual source IP | `192.0.2.40` |
| Activity type | Patient-record access |
| Investigation status | Suspicious activity; compromise not confirmed |

SupportBot accessed **1,900 patient records in four minutes**, approximately **475 records per minute**, from an unfamiliar IP address.

Although the overall weekly access volume was within the expected range, the concentration of access within four minutes and the unfamiliar source IP warrant investigation.

## 3. Security Risk Assessment

**Preliminary Severity: High**

Three factors make this event particularly concerning:

1. **Concentrated access:** A high volume of patient records was accessed within a short period, despite the weekly total remaining within its normal range.
2. **Unfamiliar source IP:** The activity originated from an IP address different from SupportBot's usual source, requiring verification of its legitimacy.
3. **Excessive permissions:** SupportBot has unrestricted patient-record access beyond its intended responsibilities, increasing the potential impact of credential misuse.

The activity could indicate unauthorised access or credential compromise. However, the available evidence does not establish who initiated the activity, whether it was authorised or whether sensitive information was exposed outside the organisation.

**Assessment:** Treat the event as a suspected security incident requiring prompt investigation, without declaring a confirmed credential compromise or data breach.

## 4. Recommended IAM Incident Response

### Step 1 — Escalate the Activity

- Create or escalate a security incident ticket.
- Notify the Security Operations Centre (SOC) or incident-response team.
- Provide the affected identity, timestamps, source IP addresses and patient-record access volume.
- Highlight SupportBot's excessive permissions and weak credential controls.

**Purpose:** Ensure the event is assessed promptly by the team responsible for incident investigation and response.

### Step 2 — Contain and Preserve Evidence

- Coordinate urgent containment of the potentially compromised credential with the authorised incident-response team and service owners.
- Revoke or disable the affected credential as directed through the approved incident-response process.
- Preserve relevant authentication records, API activity logs and incident timestamps.
- Document containment actions and verify that suspicious access has stopped.

If a replacement credential is required to restore legitimate support operations, it should be issued securely with restricted permissions through the approved incident-response process.

**Purpose:** Limit potential further access while preserving evidence needed to understand the event.

### Step 3 — Support the Investigation

- Review SupportBot's assigned permissions and credential configuration.
- Examine available authentication history and API activity for unusual access patterns.
- Check whether the unfamiliar source IP appears in other relevant records.
- Help determine which systems and records may have been accessible through the identity.
- Provide IAM evidence and findings to the incident-response team.

**Purpose:** Support the investigation into possible credential misuse, unauthorised access and potential exposure of sensitive information.

The incident-response team remains responsible for leading the broader investigation and determining whether a security breach occurred.

## 5. Additional Activity Requiring Review

The seven-day records also show actions that may not align with SupportBot's intended responsibilities.

| Activity | Security Concern | Recommended Follow-Up |
|---|---|---|
| 3 patient-contact updates | SupportBot should not independently modify patient information | Verify the changes, authorisation and affected records |
| 2 refunds ($120 and $310) | No human approval was recorded | Review the transactions and determine whether they were authorised |
| 612 outgoing emails | SupportBot is intended to draft replies for human approval | Verify whether the messages were approved before sending |

These records do not establish that the actions were malicious. However, they highlight the need to verify authorisation and strengthen oversight of sensitive activities.

Longer-term identity and access improvements are documented separately in [05 — Recommended Security Controls](05-Recommended-Security-Controls.md).

## 6. Assessment Outcome

The assessment identified unusual access to **1,900 patient records in four minutes** from an unfamiliar IP address, despite the overall weekly patient-record volume remaining within its stated normal range.

I recommended immediate escalation, coordinated containment and evidence preservation, followed by IAM support for the investigation.

The wider activity review also identified patient-data changes, refunds and outgoing emails requiring authorisation checks.

**Conclusion:** The available evidence supports investigation and risk reduction but does not confirm credential compromise or a data breach.

No incident-response actions were executed as part of this scenario-based assessment.

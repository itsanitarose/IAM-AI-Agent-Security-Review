# 02 — Permission Review

**Project:** Northwind Health | AI Agent Security Review  
**Identity:** `svc-supportbot`

---

## 1. Permission Review Overview

This assessment reviews the nine permissions currently assigned to SupportBot against its intended business responsibilities.

SupportBot is designed to answer clinic staff questions about appointment and billing status, create support tickets and draft responses for human approval.

The objective is to identify unnecessary or excessive permissions and recommend an access model based on the principle of least privilege.

## 2. Current Permission Inventory

The existing permissions assigned to SupportBot are shown below.

| # | Current Permission |
|---|---|
| 1 | Read help-centre articles |
| 2 | Read all patient records (full ePHI) |
| 3 | Read billing summaries |
| 4 | Read full billing and payment data |
| 5 | Update patient contact details |
| 6 | Issue refunds up to $500 without approval |
| 7 | Send email as `support@northwindhealth.com` |
| 8 | Create and update support tickets |
| 9 | Delete ticket history |

The inventory shows that SupportBot can access sensitive patient and financial information and perform actions beyond its stated support responsibilities.

## 3. Permission Assessment

Each permission was assessed against SupportBot's intended business purpose.

| # | Permission | Decision | Reason |
|---|---|---|---|
| 1 | Read help-centre articles | **Needed** | Required to answer routine support questions using approved information. |
| 2 | Read all patient records (full ePHI) | **Not needed** | Full patient records exceed the agent's responsibilities. |
| 3 | Read billing summaries | **Needed with conditions** | Limit access to relevant billing information for requests from authenticated and authorised clinic staff. |
| 4 | Read full billing and payment data | **Not needed** | Billing summaries are sufficient without exposing sensitive payment details. |
| 5 | Update patient contact details | **Not needed** | Requests to change patient information should be routed to an authorised human for approval. |
| 6 | Issue refunds up to $500 without approval | **Not needed** | Financial transactions require appropriate approval and accountability. |
| 7 | Send email as `support@northwindhealth.com` | **Not needed** | SupportBot should draft responses for human approval and sending. |
| 8 | Create and update support tickets | **Needed with conditions** | Restrict access and updates to authorised support workflows. |
| 9 | Delete ticket history | **Not needed** | Ticket history must be preserved for accountability and auditing. |

## 4. Proposed Access Model

I recommend restricting SupportBot's permissions to the functions necessary for its intended support role.

### Proposed Permission Matrix

**Legend:** ✓ = Retain | ◐ = Retain with conditions | — = Remove

| Permission | Proposed Access |
|---|---|
| Read help-centre articles | ✓ |
| Read all patient records (full ePHI) | — |
| Read billing summaries | ◐ |
| Read full billing and payment data | — |
| Update patient contact details | — |
| Issue refunds up to $500 without approval | — |
| Send email as support address | — |
| Create and update support tickets | ◐ |
| Delete ticket history | — |

### Access Conditions

**Billing summaries**

Access should be limited to the information necessary to answer a support request from authenticated and authorised clinic staff. SupportBot should not receive unrestricted access to billing or payment records.

**Support tickets**

SupportBot should be allowed to create support tickets and make limited updates within defined workflows. It should not be able to modify unrelated tickets or delete ticket history.

**Sensitive actions**

Requests involving patient-data changes, refunds or outgoing emails should be routed to authorised employees for approval and execution.

This approach allows SupportBot to assist with support operations without independently performing sensitive financial or data-changing actions.

## 5. Permission Review Summary

| Decision | Count |
|---|---:|
| Needed | 1 |
| Needed with conditions | 2 |
| Not needed | 6 |
| **Total** | **9** |

The assessment identifies six permissions that are not required for SupportBot's intended responsibilities and two permissions that should be retained only with appropriate restrictions.

The most significant access concerns involve unrestricted patient-record access, sensitive financial information and the ability to issue refunds without human approval.

The proposed access model reduces unnecessary permissions while preserving the functions SupportBot needs to support clinic staff.

These recommendations are based on the supplied scenario. No permissions were changed or technically tested as part of this assessment.

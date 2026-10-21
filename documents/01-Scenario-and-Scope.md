# 01 — Scenario and Scope

**Project:** Northwind Health | AI Agent Security Review  
**Focus Area:** Identity and Access Management (IAM)  
**Project Type:** Security Assessment / Security Review  
**Status:** Assessment completed

---

## 1. Business Context

Northwind Health is a fictional US-based healthcare SaaS provider supporting approximately 400 clinics with a workforce of 120 employees.

The organisation handles electronic protected health information (ePHI), making secure identity and access management essential to protecting sensitive information and supporting business operations.

### Project Scenario — The Agent With Too Many Keys

**Manager's Request**

> Support launched an AI agent called SupportBot last year. Nobody ever reviewed its access. I need you to review what it can do, tell me what's wrong with how it's set up, and check last week's activity. Then show me what it should look like.

**Business Purpose**

SupportBot is an AI-powered support agent responsible for:

- Answering clinic staff questions about appointment and billing status.
- Creating support tickets.
- Drafting responses for human approval.

**Identity Record**

| Attribute | Current State |
|---|---|
| Identity | `svc-supportbot` |
| Identity type | Service account with API token |
| Age | 14 months |
| Created by | Former contractor |
| Assigned owner | None |
| Token expiry | None |
| Token rotation | Never |
| Environments | Production and staging share the same token |
| Access review | No review since launch |

**Existing Access Concerns**

- Full patient-record access beyond its support responsibilities.
- Access to sensitive billing and payment information.
- Ability to issue refunds without approval.
- Ability to modify patient information and delete ticket history.
- Ability to send outgoing emails using the support address.

**Suspicious Activity**

On Tuesday between 03:12 and 03:16, SupportBot accessed **1,900 patient records in four minutes** from an unfamiliar IP address (`198.51.100.77`), compared with its usual source (`192.0.2.40`).

The activity requires investigation to establish whether the access was authorised and whether sensitive information was exposed. Compromise has not been confirmed.

## 2. Project Objectives

The project aims to:

1. Review SupportBot's nine permissions against its intended business responsibilities.
2. Identify identity ownership, credential lifecycle and access governance weaknesses.
3. Assess suspicious identity activity and define an appropriate IAM response.
4. Recommend least-privilege, credential security, monitoring and separation-of-duties controls.

## 3. Scope of Work

### In Scope

- SupportBot's service identity and assigned permissions.
- Non-human identity ownership and accountability.
- API token lifecycle and credential security.
- Production and staging credential separation.
- Identity and access review requirements.
- Suspicious access assessment and IAM incident-response responsibilities.
- Recommended security controls and target-state access design.

### Out of Scope

- Full forensic investigation or confirmation of a data breach.
- Changes to live healthcare production systems.
- Processing real patient information or financial transactions.
- Developing or deploying the AI support agent.
- Implementing Microsoft Entra ID controls.

## 4. Project Approach

| Stage | Activity |
|---|---|
| **Review** | Examine SupportBot's business purpose, identity record, permissions and reported activity. |
| **Identify** | Identify excessive access, missing ownership and credential governance weaknesses. |
| **Assess / Design** | Evaluate risks and determine appropriate permission restrictions and security controls. |
| **Execute / Recommend** | Recommend immediate incident-response actions and longer-term identity security improvements. |
| **Validate** | Check proposed controls and permission decisions against SupportBot's business responsibilities and the scenario evidence. |
| **Document** | Record permission decisions, governance findings, incident-response recommendations and proposed controls. |

## 5. Project Deliverables

| Deliverable | Description |
|---|---|
| **01 — Permission Review** | Assessment of nine permissions with business justification and access decisions. |
| **02 — Identity Governance Findings** | Four findings covering ownership, token lifecycle, environment separation and periodic reviews. |
| **03 — Suspicious Activity Assessment** | Evaluation of unusual identity activity and recommended escalation, containment and investigation support. |
| **04 — Recommended Security Controls** | Five controls covering credential security, ownership, least privilege, monitoring and separation of duties. |
| **05 — Job Requirements Map** | Mapping of assessment evidence to relevant IAM responsibilities and skills. |

---

**Assessment Outcome:** A documented review of SupportBot's identity security, identifying governance weaknesses, excessive access and suspicious activity, with recommendations for a more secure operating model.

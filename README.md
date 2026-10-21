# IAM AI Agent Security Review | Northwind Health

*A fictional Identity and Access Management (IAM) case study focused on AI agent permissions, non-human identity governance, credential security and suspicious activity.*

## Overview

Northwind Health is a healthcare SaaS company supporting approximately 400 clinics and handling sensitive patient information.

The Support team introduced an AI agent called SupportBot to answer appointment and billing questions, create support tickets and draft responses for human approval.

However, SupportBot's access had not been reviewed since deployment. Its service account had excessive permissions, no assigned owner and an API token that had never been rotated.

I reviewed SupportBot's nine permissions, assessed its identity governance weaknesses, examined suspicious activity and recommended controls to reduce the risks.

**The objective:** Identify unnecessary access, improve accountability for the AI agent's identity and design safer controls for its operation.

## Key Findings

| Severity | Count | Findings |
|---|---:|---|
| 🔴 High | 4 | No identity owner, non-expiring API token, shared production/staging credential and no periodic access review |
| 🔴 High | 1 | Suspicious access to 1,900 patient records in four minutes from an unfamiliar IP address |
| 🟠 Significant | — | Excessive access to patient records, payment data and refund functionality |

*Severity classifications are qualitative assessments based on the scenario. The unusual activity is an indicator of potential compromise, not confirmation of a breach.*

## Top Priority — Suspicious Patient-Record Access

On Tuesday between 03:12 and 03:16, SupportBot accessed **1,900 patient records in four minutes** from an unfamiliar IP address.

Although its weekly patient-record access was within the stated normal range, this specific activity warranted immediate investigation.

I recommended escalating the event to the incident-response team, containing the potentially compromised credential while preserving evidence, and reviewing authentication and API activity to determine the extent of possible exposure.

The available evidence does not confirm that a breach occurred.

## Project Structure

| Document | Purpose |
|---|---|
| 01 — Scenario and Scope | Defines the business context, objectives and assessment boundaries |
| 02 — Permission Review | Evaluates all nine permissions against SupportBot's intended responsibilities |
| 03 — Identity Governance Findings | Documents identity ownership, credential and access-review weaknesses |
| 04 — Suspicious Activity Assessment | Examines the unusual access event and recommended initial response |
| 05 — Recommended Security Controls | Proposes the target-state identity and access controls |
| Job Requirements Map | Connects the project evidence to relevant IAM skills |

## IAM Skills Demonstrated

- Non-human identity and service-account security assessment
- Least-privilege permission review
- API token lifecycle risk identification
- Identity ownership and access governance
- Production and staging environment separation
- Suspicious access analysis and incident-response recommendations
- Separation of duties and human approval controls
- Security documentation and risk-based recommendations

## What I Learned

This project helped me understand how IAM principles apply to AI agents, not just human users.

An AI agent may perform useful business tasks, but its identity still needs an accountable owner, appropriate permissions, secure credentials and regular reviews.

I also learned the importance of distinguishing suspicious activity from a confirmed security incident.

The area I found most challenging was understanding API token lifecycle management, particularly how expiration, rotation and revocation work in practice.

## What I Would Improve

With access to a suitable test environment, I would:

- Configure a non-human identity with restricted permissions.
- Test API token expiration, rotation and revocation.
- Validate separation between production and staging identities.
- Test whether sensitive actions require human approval.
- Review authentication and API logs to verify that monitoring controls work.

These practical exercises would help me validate the proposed controls rather than relying solely on scenario-based analysis.

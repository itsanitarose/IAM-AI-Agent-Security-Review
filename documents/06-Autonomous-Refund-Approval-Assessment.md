# Bonus: Should an AI Agent Ever Approve Refunds on Its Own?

*An AI Security and IAM Risk Assessment*

## Purpose

Assess when an AI agent should be allowed to approve refunds, when a human should decide, and when access should be denied.

## Case

- SupportBot answers billing and appointment questions, creates tickets, and drafts replies for human approval. Approving refunds is outside its role.
- It can issue refunds up to $500 without approval.
- Two refunds, $120 and $310, have no human approval recorded.
- Its identity has no owner, weak credential controls, and no access review.

These facts do not prove the refunds were fraudulent. Approving a refund and sending the money are separate actions, but both need controls.

**Project evidence:** [Scenario and Scope](01-Scenario-and-Scope.md), [Permission Review](02-Permission-Review.md), [Identity Governance Findings](03-Identity-Governance-Findings.md), and [Suspicious Activity Assessment](04-Suspicious-Activity-Assessment.md).

## Approach

Review what SupportBot needs to do, what its access allows, what could go wrong, and which controls are needed. This assessment uses the supplied scenario. The proposed controls have not been tested.

| Framework or guidance | How it supports this assessment | Source |
|---|---|---|
| NIST AI RMF | Connect the agent’s purpose, risks, controls, and ownership. | [AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) |
| OWASP Excessive Agency | Check whether the agent has more access or freedom than its role needs. | [LLM06:2025](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/) |
| MITRE ATLAS | Consider how an attacker could trick the agent into misusing its access. | [ATLAS](https://atlas.mitre.org/) |

## Risk Assessment

| Risk | Why it matters here | Required control |
|---|---|---|
| **Access beyond its role** | SupportBot can issue refunds even though its job does not include refund decisions. | Remove refund access unless the business approves a new role and checks the controls. |
| **Stolen credentials** | Someone with its token could use its refund access. No owner is assigned to manage that access. | Assign an owner, protect credentials, separate production and staging, and test that access can be removed. |
| **Wrong or manipulated decisions** | False information or malicious instructions could lead to an improper refund. No such attack is confirmed. | The billing system must check eligibility, requester access, and refund limits. Instructions to the AI are not enough. |
| **Repeated refunds and missing records** | A $500 limit does not stop many smaller refunds. Total limits and protected approval records are not shown. | Check for duplicates, limit total refunds, and keep records the agent cannot change or delete. |

## Decision and Proposed Approval Rule

**SupportBot should not approve refunds on its own in its current state.** Refund approval is outside its role, and the evidence does not show enough control over its identity or actions. Remove its refund issuance access and send refund requests to authorised billing staff.

If the business adds refund approval to its role, allow it only within clear rules:

| The agent may approve when | A human must review when |
|---|---|
| Trusted payment records confirm the claim meets the refund policy. | Information is missing, conflicting, or needs an exception. |
| The requester is allowed to request a refund for that account and payment. | The requester’s access needs checking. |
| The amount is within approved individual and total limits. | Either limit would be exceeded. |
| The refund is not a duplicate and returns to the original payment method. | A duplicate is suspected or another destination is requested. |
| The billing system checks the rules and records the approval. | The request is outside the agent’s approved role. |

**Enforcement:** The AI saying “approved” must not be enough to send money. The billing system must check the rules before accepting approval. If checks or records are unavailable, automatic processing stops. Human review must resolve missing checks before proceeding.

**Ownership and testing:** Finance sets the refund rules and limits. A named technical owner manages the agent’s access and credentials. Before access is granted, test that the system blocks unauthorised, duplicate, changed, and over-limit requests, protects records, and stops access when revoked.

**Ongoing review:** Monitor refunds and review access regularly and after changes. Suspend access if compromise is suspected or controls fail. Remove it when no longer needed. The responsible business owner must accept any remaining risk before the agent starts approving refunds.

**Autonomous refund approval should depend on a defined role, enforced limits, a named owner, and a clear record of every decision.**

# IAM: AI Agent Security Review


## The Scenario

It's my third week on the security team at Northwind Health, and the company has started introducing AI agents across its teams.

One of them, **SupportBot**, was launched to help clinic staff with appointment and billing questions, but nobody has reviewed its access since it was created.

<sub><em>* Fictional scenario. Real world analysis.</em></sub>
<br><br>


### 🎫 The Ticket

**Manager's Request:**

> "Support launched an AI agent called SupportBot last year. Nobody ever reviewed its access. I need you to review what it can do, tell me what's wrong with how it's set up, and check last week's activity. Then show me what it should look like."

## My Investigation

SupportBot operates through a service account and API token. It was created 14 months ago by a contractor who has since left, has no named owner and uses a token that never expires.

It also has nine permissions, including access to full patient records and the ability to issue refunds without human approval.

Four questions guided my investigation:

- **Does SupportBot need every permission it has?**
- **Who is responsible for an AI agent's identity and credentials?**
- **Does its recent activity suggest that something is wrong?**
- **How can we secure the agent without stopping it from helping clinic staff?**

## What I Noticed

Three findings immediately concerned me.

| Area | Finding |
|:-----|:--------|
| **Identity governance** | No named owner, no access review and a non-expiring token |
| **Excessive permissions** | Access to sensitive patient data and financial actions beyond its support role |
| **Suspicious activity** | 1,900 patient records accessed in four minutes from an unfamiliar IP address |

The last finding needed particular attention.

Tuesday's activity raised concerns about an **ongoing risk of data exfiltration** ([Fundamentals of AI Security](https://learn.microsoft.com/en-us/training/modules/fundamentals-ai-security/7-data-exfiltration) makes this really clear).

The activity doesn't match SupportBot's normal support duties, but **the evidence doesn't confirm that data was stolen**.

I would treat it as a suspected compromise, recommend immediate containment and work with the incident-response team to examine the access logs and determine what patient information may have been exposed.

## My Approach

I reviewed SupportBot's nine permissions against its actual responsibilities and examined the risks created by its identity setup.

I also researched AI agent security guidance from **Microsoft Learn** and **OWASP**, focusing on least privilege, credential security, human oversight and monitoring.

My proposed approach includes restricting sensitive data access, removing unnecessary financial authority, improving token security and introducing clear ownership and review processes.

For high-impact actions such as refunds, **SupportBot should assist with the request, while an authorised human makes the financial decision.**

## What This Case Study Covers

- A permission-by-permission review of SupportBot's access.
- Governance findings affecting its identity and API token.
- Analysis of Tuesday's suspicious activity and three immediate response actions.
- A proposed set of controls for securing the AI agent.

### What I'm Learning

I've been interested in AI security for some time, and this case study confirmed that I want to explore securing AI agents further.

I learned that managing an AI agent's identity involves more than reviewing permissions. I needed to understand how API tokens work, the difference between rotation and revocation, and why access restrictions must be enforced outside the agent.

Investigating Tuesday's activity also taught me to distinguish suspicious behaviour from a confirmed breach, and to understand where my responsibilities as an IAM analyst end and the incident-response team's begin.

The question about automated refunds pushed my thinking further. Even when AI is allowed to make decisions, an organisation cannot simply wash its hands of responsibility. Human oversight, decision records and accountability still matter.

**My biggest takeaway:** Identifying a risk is only the beginning. I want to understand how to prevent it, verify that the controls work and make sure someone remains accountable when things go wrong.

## Explore the Investigation

*Supporting documents will be linked here as the investigation develops.*

<br>

---

[← Week 2: Permission Sprawl & RBAC](https://github.com/itsanitarose/IAM-Permission-Sprawl-RBAC) · [All Case Studies](https://github.com/itsanitarose/IAM-Case-Studies)

*Northwind Health is fictional. This is independent work. No production systems were changed.*

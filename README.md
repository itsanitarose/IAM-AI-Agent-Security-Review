
# IAM: AI Agent Security Review

## 🎫 The Ticket

It's 19 October 2026, my third week on the security team at Northwind Health. This time, the ticket concerns SupportBot, an AI agent introduced to help clinic staff with appointment and billing questions.

The IT Manager writes:

> Support launched an AI agent called SupportBot last year. Nobody ever reviewed its access. **I need you to review what it can do, tell me what's wrong with how it's set up, and check last week's activity. Then show me what it should look like.**

<br>

This isn't a normal access review. There's no person on the other end. So what exactly am I dealing with?

<br>

## My Investigation

Until now, every account I've reviewed had a person behind it. SupportBot is different.

There are three things I need to separate:

- **SupportBot:** The AI agent carrying out the work.
- **`svc-supportbot`:** The service account it operates through.
- **API token:** The credential used to authenticate its requests.


Keeping them clear helps me see what is what.

<br>

I started with SupportBot's [identity record](Document/01.%20Source%20Data.md), then checked its [permissions](Document/02.%20Permission%20Review.md). The problem became clearer: an agent with no named owner, a token that never expires, and permissions that go beyond its support role.

That left me with four questions:

1. Does SupportBot need every permission it has?
2. Who is responsible for its identity and credentials?
3. Does its recent activity suggest something is wrong?
4. How can I secure the agent without stopping it from helping clinic staff?



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

*<sub>Northwind Health is fictional. This is independent work. No production systems were changed.</sub>*

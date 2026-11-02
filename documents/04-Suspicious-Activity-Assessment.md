# 04. Suspicious Activity & Incident Response

## 1. Investigating Tuesday's Activity

After reviewing SupportBot's permissions and identity governance, Tuesday's activity became my most urgent concern.

Here is what the logs showed:

| Evidence | Recorded Activity |
|:---------|:------------------|
| **Day** | Tuesday |
| **Duration** | Four minutes |
| **Patient records accessed** | 1,900 |
| **Source IP** | `198.51.100.77` |
| **Normal SupportBot IP** | `192.0.2.40` |

Two things immediately raised concerns: **the unfamiliar IP address and the speed of access**.

SupportBot normally answers individual clinic questions. Accessing 1,900 patient records in four minutes doesn't fit that behaviour.

The weekly total of 38,400 records falls within the normal range of 35,000 to 45,000. But a normal weekly total doesn't explain an unusual burst of activity.

## 2. What Could This Mean?

One possible explanation is that someone used SupportBot's credentials to retrieve patient records in bulk. The unfamiliar IP address and rapid access make credential misuse a concern, but they don't establish who made the requests or why.

While researching this risk, I referred to Microsoft's [Fundamentals of AI Security](https://learn.microsoft.com/en-us/training/modules/fundamentals-ai-security/7-data-exfiltration) material on data exfiltration. It helped me understand how an AI agent's access to sensitive information could potentially be abused.

I would treat this as a possible compromise requiring urgent investigation. However, the evidence doesn't confirm that the token was stolen, that the requests were unauthorised or that patient information reached someone who shouldn't have it.

## 3. My First Three Actions

| Priority | Action | What I Would Do |
|:---------|:-------|:----------------|
| **1** | **Contain suspected access** | Immediately alert IT and the incident-response team. Recommend revoking the potentially compromised token and temporarily disabling SupportBot's access. Ask for confirmation that containment has been applied. |
| **2** | **Preserve and scope the evidence** | Request preservation of relevant authentication, API access and audit logs. Share the account details, recorded activity window and unfamiliar IP address so investigators can determine which records were accessed and whether other suspicious activity occurred. |
| **3** | **Escalate possible patient-data exposure** | Raise or update the security incident and flag the possible ePHI exposure to the appropriate Privacy or Compliance team through the incident process. Provide my IAM findings to support their assessment. |

**My priority would be to stop possible misuse of SupportBot's identity while making sure the incident response team has the evidence it needs.**

These actions should be coordinated urgently. Preserving evidence and escalating the incident shouldn't have to wait until containment is complete.

## 4. My Assessment

**I wouldn't wait for confirmation of a breach before recommending containment.**

Disabling SupportBot could temporarily slow down clinic support, but leaving potentially compromised access active could put more patient information at risk. I would recommend that the Support team handle requests manually until IT confirms the agent can safely return to service.

The incident response team would lead the wider investigation. My role would be to support them with identity, permission and available authentication evidence.

Once the immediate risk is addressed, I would turn to the longer term weaknesses identified in my assessment.

**Document 05: Security Controls & Target State** explains how I would recommend securing SupportBot's identity, credentials and permissions to reduce the chance of the same problems happening again.



---

[Back to Project Overview](https://github.com/itsanitarose/IAM-Agent-With-Too-Many-Keys)

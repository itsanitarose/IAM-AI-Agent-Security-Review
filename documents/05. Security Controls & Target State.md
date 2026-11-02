# 05. Security Controls & Target State

## 1. Designing Safer Access for SupportBot

After reviewing SupportBot's permissions, identity governance and suspicious activity, I wanted to understand what a safer setup would look like.

My aim isn't to stop the agent from helping clinic staff. It's to give SupportBot **only the access it needs**, make someone accountable for that access and ensure sensitive actions can't happen without proper authorisation.

I used the [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html) and [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html) to help turn the risks I identified into practical recommendations.

## 2. My Recommended Security Controls

| Control | My Recommendation | Why It Matters |
|:--------|:------------------|:---------------|
| **1. Assign ownership and review access** | Give SupportBot a named internal owner and an identity expiry or review date. Include it in quarterly access reviews and review permissions whenever its responsibilities change. | AI agents are non-human identities. They need clear accountability and regular reviews, just like other service accounts. |
| **2. Separate and secure credentials** | Create separate service identities for production and staging. Store secrets in an approved vault, automate rotation where supported and restrict access from unexpected networks or IP addresses. Revoke the old shared token in both environments. | A credential exposed in staging shouldn't also work in production. Secure storage and credential controls reduce the opportunity for misuse. |
| **3. Use short-lived, task-scoped access** | Use short-lived, narrowly scoped credentials where supported. For patient-data requests, the application must verify the requesting staff member's access and return only the clinic, patient and fields needed for that request. Where supported, use delegated access so requests are made on behalf of the staff member rather than through unrestricted application access. | Credential expiry limits how long access lasts, while application authorisation controls which information can be retrieved. Both are needed to reduce unnecessary exposure. |
| **4. Keep sensitive actions under human control** | Keep patient and billing access read-only. Permit support-ticket creation and limited updates, but remove SupportBot's ability to issue refunds, change patient contact details, send emails independently or delete ticket history. Allow it to draft replies, with authorised staff approving and carrying out sensitive actions through enforced workflows. | SupportBot can handle its intended support tasks without independently making financial decisions or changing sensitive patient information. |
| **5. Log and monitor every action** | Record authentication, API requests and agent actions against SupportBot's identity, with the associated requester and support request where available. Alert on bulk patient-record reads, unexpected source IPs and activity outside agreed operating hours, where applicable. Protect audit records from unauthorised changes and avoid recording API tokens or unnecessary patient information. | Monitoring helps the security team identify suspicious behaviour. Protected audit records provide reliable evidence without creating another source of sensitive-data exposure. |

## 3. What SupportBot Should Be Allowed to Do

I would keep SupportBot focused on its original responsibilities.

| Task | Target Access |
|:-----|:--------------|
| Answer general support questions | Read approved help-centre articles. |
| Answer appointment or billing-status questions | Read only the necessary information after the application verifies the requesting staff member's access. |
| Create and update support tickets | Use restricted permissions to create tickets and make permitted updates relevant to the support request. |
| Respond to clinic staff | Draft replies for an authorised human agent to approve and send. |
| Issue refunds | No direct permission. Refunds remain with authorised staff under the appropriate approval process. |
| Update patient contact details or delete ticket history | No permission. These actions remain outside SupportBot's role. |

This would allow SupportBot to perform its intended support duties without retaining unnecessary authority over patient records or financial transactions.

## 4. How I Would Verify the Controls

I wouldn't consider these recommendations complete just because new permissions and policies had been configured.

As an IAM analyst, I would review the updated identity and access settings and work with IT, application and security teams to verify that:

- The old shared API token has been revoked and is rejected in both production and staging.
- Production and staging use separate identities and credentials, and staging credentials cannot be used in production.
- SupportBot has a named owner, an identity review date and a scheduled quarterly access review.
- SupportBot can still answer authorised status questions, create support tickets and make permitted ticket updates.
- A staff member cannot use SupportBot to retrieve information about a patient or clinic they are not authorised to access.
- Short-lived credentials stop working after expiry, where implemented.
- Attempts to issue refunds, change patient details, send emails directly or delete ticket history are denied.
- Unusual bulk access and requests from unexpected sources generate the expected logs and alerts.
- Audit records contain the identifiers needed for investigation without exposing tokens or unnecessary patient information.

**The important part is checking that restrictions are actually enforced**, not simply documenting what SupportBot is supposed to do.

## 5. Final Assessment

**My recommendation is to retain SupportBot as a support assistant, with restricted access, clear ownership and independently enforced authorisation.**

The proposed controls would reduce the risk of credential misuse and unnecessary exposure of patient information while preserving the agent's intended support functions.

These controls would need to be implemented and tested by the relevant teams before SupportBot could be considered ready for a secure return to service.


---

[Back to Project Overview](https://github.com/itsanitarose/IAM-AI-Agent-Security-Review)


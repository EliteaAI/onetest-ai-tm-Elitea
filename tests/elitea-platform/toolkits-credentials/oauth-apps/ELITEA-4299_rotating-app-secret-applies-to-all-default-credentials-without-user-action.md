---
id: ELITEA-4299
title: "Rotating the app secret applies to every Default app credential; changing the client asks users to sign in again"
priority: high
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:admin-platform, int:oauth, nfr:security, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4299: Rotating the app secret applies to every Default app credential; changing the client asks users to sign in again

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify the acceptance criterion "rotating the secret in the Admin Portal takes effect for all Default-mode credentials without user action", and that a change of client ID, tenant or scopes is picked up on the next sign-in.

---

## Preconditions

- App **PUB** (Public, Default). Two valid secrets **S1** (current) and **S2** for it.
- Users U1 and U2, each with a signed-in Default Outlook credential and an agent using it. Auto refresh token on.
- Optional: a second Entra app **APP2** (client ID + secret) and a second tenant.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | U1 and U2 run their agents with "Read my latest email". | Both work. |
| 2 | As Admin, edit PUB → Replace → S2 → Save. | "App updated. Credentials that use it pick up the change." |
| 3 | Wait for (or force) a token refresh; U1 and U2 run their agents again. | Both work. **No** new sign-in asked, no credential edit. |
| 4 | Replace with an invalid secret and Save. Force a token refresh / new sign-in for U1. | Sign-in / refresh fails with a readable error. No secret value in the error. |
| 5 | Restore S2. U1 runs again. | Works without user action. |
| 6 | (APP2) Change PUB's Client ID to APP2's and Replace with APP2's secret. U1 runs the agent. | U1 is asked to **sign in again once** (old token belongs to the old client and is not used). After sign-in, works. Consent shows APP2. |
| 7 | (Second tenant) Set PUB's endpoint to `…/<tenant_A>` (with secret). U2 from tenant B signs in. | U2 can't sign in (tenant mismatch from Microsoft). A user from tenant A can. |
| 8 | Restore the endpoint to `…/organizations`. Add **Mail.Send** to PUB's Outlook scopes. U1 signs in again. | Consent asks for Mail.Send. A "send email" prompt works. |

---

## Postconditions

- Restore PUB to the original client, endpoint, scopes and a valid secret.

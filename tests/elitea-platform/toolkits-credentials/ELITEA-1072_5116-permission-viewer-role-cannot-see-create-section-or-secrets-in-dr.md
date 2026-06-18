---
id: ELITEA-1072
title: "[EliteaAI/elitea_issues#5116] Permission: Viewer Role Cannot See CREATE Section or Secrets in Dropdown"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:settings, nfr:security, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-1072: [EliteaAI/elitea_issues#5116] Permission: Viewer Role Cannot See CREATE Section or Secrets in Dropdown

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that a user with only the Viewer role on a team project sees neither the CREATE section nor any saved secrets in the credential secret dropdown — the dropdown must be empty or fully restricted for Viewers.

## Preconditions

- A team project has at least one saved project secret
- A second test user account exists with only the Viewer role on that team project (no secret create or list permissions)
- Logged in as the Viewer user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as the Viewer role user on the team project. | Viewer user is logged in and on the team project. |
| 2 | Navigate to Configuration → Credentials in the team project. | Credentials page loads. |
| 3 | Click Create Credential and select GitHub (or any toolkit with a token/secret field — e.g., Jira or Confluence if GitHub is unavailable). Select Token auth type. | Credential creation form opens with the token field visible. |
| 4 | Switch the token field to Secret mode. | Token field switches to Secret mode; combobox appears. |
| 5 | Open the secret selection dropdown. | Dropdown opens. |
| 6 | Inspect the dropdown content. | (1) No CREATE section is visible — no 'New Project Secret' or 'New Private Secret' option shown. (2) No saved secrets are listed in SAVED SECRETS — Viewer cannot list project secrets. (3) No JavaScript errors in console. (4) No error toast or crash from simply opening the dropdown. |

## Expected Final State

(1) No CREATE section is visible — no 'New Project Secret' or 'New Private Secret' option shown. (2) No saved secrets are listed in SAVED SECRETS — Viewer cannot list project secrets. (3) No JavaScript errors in console. (4) No error toast or crash from simply opening the dropdown.

## Pass/Fail Criteria

**Pass:** Viewer sees no CREATE button and no saved secrets in the dropdown — field shows empty/restricted state.
**Fail:** Viewer can see the CREATE button (privilege escalation); Viewer can see the list of project secrets (data exposure); application crashes or shows unhandled error on dropdown open.

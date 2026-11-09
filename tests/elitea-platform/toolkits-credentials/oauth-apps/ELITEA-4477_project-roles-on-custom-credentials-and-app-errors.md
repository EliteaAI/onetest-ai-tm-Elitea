---
id: ELITEA-4477
title: "Project roles on Custom app credentials and on credentials whose app became unavailable"
priority: high
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, nfr:security, int:oauth, int:teams, issue:7149, issue:7384, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4477: Project roles on Custom app credentials and on credentials whose app became unavailable

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify the role rules when no app applies (Custom app only) and when a team credential's app is disabled: only editors and admins can fix the credential, only admins can sign in on it again, and viewers see the error read-only.

---

## Preconditions

- Apps **APP_1** and **APP_2** on **Project 1**, enabled, not Default. No app for team project **pr_R**.
- Users **V** (viewer), **E** (editor), **A** (admin) in pr_R.
- Team Teams credential `tm_team_4477` saved on **APP_2**, signed in by A.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Admin (platform), disable APP_2. As **V**, open `tm_team_4477`. | Shows "APP_2 was disabled by your administrator. Switch to Custom app." Read-only: V can't change the app or switch to Custom. |
| 2 | As **E**, open it, pick APP_1, Save. | Saved. |
| 3 | As E, sign in on it again. | 403 "Only project admins can log in or out on a team credential". |
| 4 | As **A**, sign in. | Success: agent runs with the credential work again. |
| 5 | Disable APP_1 too (no app applies). As E, New → Teams, fill Client ID, secret, endpoint. | Plain Custom form; **Save is active** (bug #7384) and saves. |
| 6 | As V, open New → Teams. | Not allowed (no create button / 403 on API POST). |
| 7 | As E, switch `tm_team_4477` to **Custom app**, fill own client, Save. | Saved. GET: own `client_id`, no `oauth_app_id`. |
| 8 | As A, re-enable APP_2. As V, E and A reopen `tm_team_4477`. | Switcher with Custom app preselected for all; only E and A can change it. |

---

## Postconditions

- Re-enable APP_1, delete test credentials.

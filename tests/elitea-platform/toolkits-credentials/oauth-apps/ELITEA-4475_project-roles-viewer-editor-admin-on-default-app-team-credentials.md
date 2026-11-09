---
id: ELITEA-4475
title: "Project roles on Default app team credentials: viewer, editor and admin"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, nfr:security, int:oauth, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4475: Project roles on Default app team credentials: viewer, editor and admin

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify what each project role can do with a Teams / Outlook / SharePoint **team** credential in Default app mode: viewers can only see it, editors can create and edit it but not sign in on it, and project admins can do everything including sign-in. No role gets the app secret.

---

## Preconditions

- App **PUB** on **Project 1**, **Default**, all 3 types. No app for team project **pr_R**.
- Three users in pr_R: **V** (viewer), **E** (editor), **A** (project admin), each with a Microsoft account.
- None of them is an Administration (platform) admin.

---

## Test Data

| Item | Value |
|------|-------|
| Team credential | Outlook, `ol_team_4475`, created by A |
| Sign-in denied text | "Only project admins can log in or out on a team credential" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As **V**, open pr_R → Credentials. | List opens. `ol_team_4475` is visible. No "+ Create" / New button (or it is disabled). |
| 2 | As V, open `ol_team_4475`. | Read-only view: "Sign-in settings are managed by your administrator."; no Save, no Delete. |
| 3 | As V, call `GET /api/v2/configurations/oauth_apps/{pr_R}?type=outlook`. | 200 with PUB, `mode: "default"`, no `client_secret`. |
| 4 | As V, POST a Teams credential and PUT / DELETE `ol_team_4475` via API. | 403 for each. |
| 5 | As **E**, Credentials → New → Outlook, name only, Save. | Saved (Default app mode). GET: `oauth_app_id` = PUB, no secret. |
| 6 | As E, edit `ol_team_4475` (display name) and Save. | Saved. |
| 7 | As E, open the credential's sign-in (Login) and complete the Microsoft login. | Saving the login is **refused**: "Only project admins can log in or out on a team credential" (403). No stored login on the credential. |
| 8 | As E, look for Shared on the form. | Not offered. API PUT with `shared: true` → 400 "Outlook credentials cannot be shared". |
| 9 | As **A**, sign in on `ol_team_4475`. | Success. The proxy call has `oauth_app_id` + `credential_type`, no secret. The credential now has a stored login. |
| 10 | As A, log out (clear the login) on the credential. | Allowed. As E, try the same after A signs in again → 403 with the same text. |
| 11 | As V, run an agent in pr_R that uses a toolkit with `ol_team_4475` (if viewers can chat). | **Record**: the run uses A's stored login (team credential), or asks V to sign in. |
| 12 | As A, delete the credential E created. | Deleted. |
| 13 | As V, E and A, open Admin Portal → Configuration. | No OAuth Apps section (they aren't platform admins). Admin API `/api/v2/admin/oauth_apps/administration` → 403. |
| 14 | Repeat steps 5 – 9 for **Teams** and **SharePoint** (Delegated). | Same role rules. |

---

## Postconditions

- Delete `ol_team_4475` and other test credentials.

---
id: ELITEA-4305
title: "OAuth Apps — Default App Credential Saves With a Name Only and Stores No Client Fields"
priority: critical
type: regression
module: toolkits-credentials/oauth-apps
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:credentials, nfr:security, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4305: OAuth Apps — Default App Credential Saves With a Name Only and Stores No Client Fields

**Module:** toolkits-credentials/oauth-apps · **Priority:** critical · **Type:** regression

**Objective:** Regression of saving a credential in Default app mode: only a name is needed, there is no unsaved-changes warning, only the app reference is stored, and no secret is returned. The Microsoft sign-in itself is not part of this case. Manual source: ELITEA-4295.

---

## Preconditions

- One enabled app on Project 1, marked **Default** (created by API).
- A project user logged in to the UI.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Credentials → New → Outlook. | No switcher. Save is disabled before typing. |
| 2 | Enter a display name and Save. | Saved, back to the list. **No** unsaved-changes warning. |
| 3 | GET the credential via API. | `oauth_app_id` = the app's id. No `client_secret` value in the response. |
| 4 | Open the credential and leave without edits. | No unsaved-changes warning. |
| 5 | Create an Outlook toolkit with the credential and open its sign-in window. | Scope is read-only, tooltip "Set by your administrator for the default app." |
| 6 | Start the sign-in and capture the requests (don't complete the Microsoft login). | The authorize URL uses the app's client ID. No client secret in any request or response. |

---

## Expected Final State

The credential references the admin app only.

## Teardown

Delete the toolkit, the credential and the app.

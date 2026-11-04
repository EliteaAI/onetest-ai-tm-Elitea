---
id: ELITEA-4386
title: "OAuth Apps — Private Default App Credential Is Selectable in a Team Project Toolkit"
priority: high
type: regression
module: toolkits-credentials/oauth-apps
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:credentials, feat:toolkits, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4386: OAuth Apps — Private Default App Credential Is Selectable in a Team Project Toolkit

**Module:** toolkits-credentials/oauth-apps · **Priority:** high · **Type:** regression

**Objective:** Regression of using a private Default app credential in a team project toolkit, without the Microsoft sign-in: the private credential is offered and marked private, sign-in settings come from the admin app, and other members don't get it. Manual source: ELITEA-4381.

---

## Preconditions

- One enabled app on Project 1 marked **Default**, Outlook on (by admin API). No app for the team project.
- Users U1 and U2, editors in the team project.
- An Outlook toolkit in the team project that refers to credential ID `at_private_<timestamp>`.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, in the Private project create an Outlook credential with that ID (Default app, name only). | Saved; GET shows `oauth_app_id` = the app. |
| 2 | As U1, open the team toolkit → Configuration. | U1's private credential is selected and marked private. No missing-credential banner. |
| 3 | Open the toolkit sign-in window. | Scope is read-only, tooltip "Set by your administrator for the default app." |
| 4 | Start the sign-in and capture the requests (don't complete the Microsoft login). | Authorize URL uses the app's client ID. No client secret in any request or response. |
| 5 | As U2 (no private credential), open the same toolkit. | Missing-credential banner; U1's credential is not offered. |

---

## Expected Final State

The team toolkit uses each member's own private credential only.

## Teardown

Delete the credential, the toolkit and the app.

---
id: ELITEA-4306
title: "OAuth Apps — Credential Shows the Reason When Its App Is Disabled, Then Recovers"
priority: high
type: regression
module: toolkits-credentials/oauth-apps
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:credentials, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4306: OAuth Apps — Credential Shows the Reason When Its App Is Disabled, Then Recovers

**Module:** toolkits-credentials/oauth-apps · **Priority:** high · **Type:** regression

**Objective:** Regression of a credential whose admin app becomes unavailable: the form shows the reason and the user can pick another app. Re-enabling the app restores the credential. Manual source: ELITEA-4292, ELITEA-4298.

---

## Preconditions

- Two enabled non-default apps on Project 1: **APP_1** and **APP_2** (created by API).
- A project user has an Outlook credential saved on **APP_2**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Disable APP_2 (API). Open the credential. | App field is empty, with "APP_2 was disabled by your administrator. Switch to Custom app." |
| 2 | Open the App dropdown. | Only APP_1 is listed. |
| 3 | Switch Outlook off on APP_1 (API). Reload. | Plain Custom form (no app applies to Outlook). Switch Outlook on again. |
| 4 | Re-enable APP_2 (API). Reload the credential. | No error. APP_2 is selected again with no user edit. |
| 5 | Delete APP_2 (API). Reload. | Error that the app no longer exists, with "Switch to Custom app." |
| 6 | Pick APP_1 and Save. | Saved. GET shows `oauth_app_id` = APP_1. |

---

## Expected Final State

The credential uses APP_1.

## Teardown

Delete the credential and APP_1.

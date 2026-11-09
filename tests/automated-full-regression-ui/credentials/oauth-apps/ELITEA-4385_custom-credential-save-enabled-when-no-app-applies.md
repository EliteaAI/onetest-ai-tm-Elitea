---
id: ELITEA-4385
title: "OAuth Apps — Custom Credential Save Is Enabled When All Apps Are Disabled"
priority: critical
type: regression
module: toolkits-credentials/oauth-apps
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:credentials, int:outlook, int:teams, issue:7384, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7384", "EliteaAI/elitea_issues#7149"]
---

# ELITEA-4385: OAuth Apps — Custom Credential Save Is Enabled When All Apps Are Disabled

**Module:** toolkits-credentials/oauth-apps · **Priority:** critical · **Type:** regression

**Objective:** Regression for bug #7384: with every Entra ID app disabled, the Outlook and Teams Custom app form enables Save once the required fields are filled and saves the credential. Manual source: ELITEA-4384.

---

## Preconditions

- All OAuth apps disabled (by admin API).
- A project user logged in to the UI.

---

## Test Data

| Field | Value |
|-------|-------|
| Display name / ID | `at_custom_<timestamp>` |
| Client ID | any GUID |
| Client secret | any non-empty string |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Credentials → New → Outlook. | Plain Custom app form, no switcher. Save disabled. |
| 2 | Fill Display name, ID, Client ID and Client secret. | Save is **enabled**. |
| 3 | Clear Client secret. | Save disabled. Refill: enabled. |
| 4 | Click Save. | Saved, back to the list, no warning. |
| 5 | GET the credential via API. | Own `client_id` stored, no `oauth_app_id`. |
| 6 | Repeat steps 1 – 4 for Teams. | Same result. |

---

## Expected Final State

Both credentials exist with their own client.

## Teardown

Delete the credentials; restore the apps' previous enabled state.

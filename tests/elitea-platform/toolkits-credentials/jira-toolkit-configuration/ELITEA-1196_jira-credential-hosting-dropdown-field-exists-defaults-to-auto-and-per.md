---
id: ELITEA-1196
title: "Jira Credential — Hosting Dropdown Field Exists, Defaults to Auto, and Persists All Three Values"
priority: high
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, int:jira, r-2.0.2]
requirements: []
---
# ELITEA-1196: Jira Credential — Hosting Dropdown Field Exists, Defaults to Auto, and Persists All Three Values

**Module:** Jira Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Hosting dropdown field is present on the Jira credential configuration form, appears before Base URL, has the correct options (Auto, Cloud, Server) with Auto as default, shows an ℹ️ tooltip, and that the selected value is saved and displayed correctly after saving.

**Coverage:**
- Hosting field present before Base URL in the credential form
- Default value is Auto
- All three options are selectable: Auto, Cloud, Server
- ℹ️ info icon is present next to the Hosting label
- Selected value persists after saving and reloading the credential

## Preconditions

- Logged in to {{base_url}}
- Access to Private or Team project credentials page
- Ability to create or edit a Jira credential

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the credentials configuration and open (or create) a Jira credential. Inspect the form layout. | A **Hosting** dropdown field is present in the form. It appears before the Base URL field. An ℹ️ icon is visible next to the Hosting label. |
| 2 | On a new Jira credential, check the default selected value of the Hosting dropdown without changing anything. | The Hosting field defaults to **Auto**. |
| 3 | Click the Hosting dropdown and inspect the available options. | The dropdown contains exactly three options: **Auto**, **Cloud**, **Server**. |
| 4 | Select **Cloud**, fill in the required fields (Display Name, Base URL, credentials), and save the credential. Reopen the credential. | The Hosting field shows **Cloud** after reopening — the value was persisted correctly. |
| 5 | Edit the same credential, change Hosting to **Server**, save, and reopen. | The Hosting field shows **Server** after reopening — the value was persisted correctly. |
| 6 | Edit the same credential, change Hosting back to **Auto**, save, and reopen. | The Hosting field shows **Auto** after reopening — the value was persisted correctly. |

## Expected Final State

The Hosting field shows **Auto** after reopening — the value was persisted correctly.

## Pass/Fail Criteria

**Pass:**
- Hosting dropdown is present before Base URL in the Jira credential form
- Default value is Auto on a new credential
- All three options (Auto, Cloud, Server) are available in the dropdown
- ℹ️ icon is visible next to the Hosting label
- Each selected value is correctly saved and displayed on credential reload

**Fail:**
- Hosting field is absent from the credential form
- Default is not Auto
- Any option is missing from the dropdown
- Selected value reverts to a different value after saving

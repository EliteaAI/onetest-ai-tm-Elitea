---
id: ELITEA-3517
title: "Outlook Toolkit Is Selectable and Links to an Outlook Credential"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3517: Outlook Toolkit Is Selectable and Links to an Outlook Credential

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Outlook" appears in the Toolkit type selector, and the toolkit form's `outlook_configuration` field only accepts Outlook-type credentials.

## Preconditions

- At least one authorized Outlook credential exists (per ELITEA-3504)

## Test Data

- Toolkit name: `outlook-toolkit-e2e`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → Create Toolkit | Type selector opens |
| 2 | Locate "Outlook" in the selector | Outlook is listed with its own icon/label |
| 3 | Select "Outlook" and open the Configuration dropdown | Only Outlook-type credentials are listed as selectable, not SharePoint/Teams/other credential types |
| 4 | Select an existing Outlook credential and name the toolkit `outlook-toolkit-e2e` | Credential is attached to the toolkit |
| 5 | Save the toolkit | Toolkit `outlook-toolkit-e2e` is created successfully |

## Expected Final State

An Outlook toolkit exists, correctly linked to the selected Outlook credential.

## Pass/Fail Criteria

**Pass:**
- Outlook is selectable as a toolkit type
- Configuration dropdown filters to Outlook credentials only
- Toolkit saves successfully with the credential attached

**Fail:**
- Outlook missing from toolkit type selector
- Non-Outlook credentials appear as selectable in `outlook_configuration`
- Save fails despite valid configuration

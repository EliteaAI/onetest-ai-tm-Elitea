---
id: ELITEA-1224
title: "SharePoint Toolkit — Existing Toolkit Backward Compatibility After Feature Deployment"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1224: SharePoint Toolkit — Existing Toolkit Backward Compatibility After Feature Deployment

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that a SharePoint toolkit created before the Site Path feature continues to function correctly with no regression after R-2.0.4 deployment. Covers: pre-existing toolkit loads without errors; Site Path field is present but empty; Get files list and Read document operate using the credential's original /sites/ URL.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- An existing SharePoint toolkit created before R-2.0.4 (no Site Path populated)
- SharePoint credential with a full /sites/ URL (e.g., https://5clkvm.sharepoint.com/sites/TestSite)
- At least one document available at that site

## Test Data

- Existing toolkit name: Sharepoint regression (pre-feature)
- Credential Site URL: https://5clkvm.sharepoint.com/sites/TestSite
- Document path: a valid server-relative path in the /sites/ library

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits and open the existing pre-feature SharePoint toolkit. | Toolkit Configuration page loads. No JSON parse errors, no 'Toolkit must have settings field' banner, no blank sections. |
| 2 | Inspect the CONFIGURATION section in Form view. | The Site Path field is visible and empty. All other fields (Name, Credential, PgVector, Tools) are unchanged. |
| 3 | Open Raw JSON view. | JSON does not contain a site_path key, OR contains "site_path": null / "site_path": "". No schema errors. |
| 4 | In the Test Settings panel, select the Get files list tool. Click Run Tool. | Files from the credential's /sites/TestSite URL are returned. No 'site not found', no HTTP 4xx/5xx error. |
| 5 | Select the Read document tool. Provide a valid document path from the same site. Click Run Tool. | Document content is returned. No errors. Content matches the document in the /sites/ library. |

## Expected Final State

Document content is returned. No errors. Content matches the document in the /sites/ library.

## Pass/Fail Criteria

Pass:
- Configuration page loads cleanly with Site Path field empty
- Get files list and Read document both return correct data from the original /sites/ URL
- No behavioral regression or new errors introduced

Fail:
- Configuration page shows errors, blank sections, or JSON schema problems
- Tools fail or return data from a wrong site
- Site Path field causes a validation error when empty on a pre-existing toolkit

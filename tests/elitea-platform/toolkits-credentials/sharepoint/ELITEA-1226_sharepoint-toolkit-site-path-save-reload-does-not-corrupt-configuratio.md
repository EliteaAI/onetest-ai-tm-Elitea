---
id: ELITEA-1226
title: "SharePoint Toolkit — Site Path Save/Reload Does Not Corrupt Configuration"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1226: SharePoint Toolkit — Site Path Save/Reload Does Not Corrupt Configuration

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify the full save → reload lifecycle for a toolkit with Site Path set produces no data loss, JSON errors, or broken tool execution. Covers: Site Path teams/ value persists; Raw JSON and Form view stay in sync; Site Path can be updated and cleared without errors.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with a tenant-only credential URL (e.g., https://your-tenant.sharepoint.com)
- Both teams/TestTeam and sites/AnotherSite are accessible on the tenant

## Test Data

- Toolkit: any existing SharePoint toolkit using the tenant-only credential
- Site Path value 1: teams/TestTeam
- Site Path value 2: sites/AnotherSite
- Site Path value 3: empty string

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the SharePoint toolkit in Edit mode. Set Site Path to teams/TestTeam. Click Save. | Save completes with no error toast or modal. |
| 2 | Close the toolkit detail page. Re-open the same toolkit. | Configuration page loads. Site Path field shows teams/TestTeam. |
| 3 | Switch to Raw JSON view. | JSON contains "site_path": "teams/TestTeam". No other fields are altered. |
| 4 | In Test Settings, select Get files list, click Run Tool. | Files from the /teams/TestTeam site are returned. No HTTP errors. |
| 5 | Switch back to Form view. Change Site Path to sites/AnotherSite. Click Save. Re-open the toolkit. | Site Path shows sites/AnotherSite. Raw JSON shows "site_path": "sites/AnotherSite". |
| 6 | Clear the Site Path field (empty). Click Save. Re-open the toolkit. | Site Path field is empty. No validation error shown. |
| 7 | In Test Settings, select Get files list, click Run Tool. | Files returned from the credential's default URL (tenant fallback). No errors. |

## Expected Final State

Files returned from the credential's default URL (tenant fallback). No errors.

## Pass/Fail Criteria

Pass:
- Each value persists correctly across save/reload
- Raw JSON and Form view remain in sync
- Tools execute without errors at each Site Path value
- Clearing to empty causes no validation error and restores credential-URL fallback

Fail:
- Any save silently discards the Site Path value
- Raw JSON and Form view are out of sync
- A non-empty Site Path from a prior save leaks into a subsequent empty-save state
- Tool execution fails or crashes after any lifecycle step

---
id: ELITEA-1714
title: Verify ability to delete PGVector credentials from Settings
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1714: Verify ability to delete PGVector credentials from Settings

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that PGVector credentials can be deleted from Settings with proper confirmation dialog, and deleted credentials no longer appear in toolkit dropdowns.


## Preconditions

- User is logged in to `{{base_url}}`
- At least one unused PGVector credential exists (not assigned to any agent)
- User has permissions to delete integrations

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Credential to Delete | [unused test credential] |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | Page loads |
| 2 | Locate a PGVector credential that is NOT in use by any agent | Unused credential is visible |
| 3 | Click "Delete" icon/button for the credential | Confirmation dialog appears: "Are you sure?" |
| 4 | Confirm deletion | Credential is removed; success message appears |
| 5 | Verify credential is removed from the list | Credential no longer appears in AI Configuration list |
| 6 | Navigate to agent configuration, open PGVector dropdown | Agent config loads |
| 7 | Check PGVector dropdown | Deleted credential does NOT appear in dropdown |

## Expected Final State

PGVector credential is successfully deleted from Settings and no longer appears in toolkit dropdowns.

## Pass/Fail Criteria

**Pass:**
- Delete button/icon is available
- Confirmation dialog appears on delete
- Credential is removed after confirmation
- Success message appears
- Credential no longer in AI Configuration list
- Credential no longer in toolkit dropdown
- If credential is in use, deletion is prevented with warning

**Fail:**
- Delete functionality is missing or broken
- No confirmation dialog
- Credential not removed
- No success message
- Credential still appears in lists
- In-use credentials can be deleted without warning

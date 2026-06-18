---
id: ELITEA-1267
title: "Scopes Field — Accepts Comma and Space-Separated Values"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1267: Scopes Field — Accepts Comma and Space-Separated Values

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Scopes field in Delegated auth mode correctly accepts both comma-separated and space-separated scope values, and that all provided scopes are passed to the OAuth flow.

**Coverage:**
- Comma-separated scopes: `sites.read.all, user.read, files.read.all`
- Space-separated scopes: `sites.read.all user.read files.read.all`
- Mixed separator: `sites.read.all, user.read files.read.all`
- Scopes are correctly forwarded to the Microsoft identity platform during Login
- Hint text "Enter scopes separated by commas or spaces" is visible

## Preconditions

- Logged in to `{{base_url}}
- SharePoint credential form open in Delegated mode

## Test Data

- Scopes comma: `sites.read.all, user.read, files.read.all, sites.selected`
- Scopes space: `sites.read.all user.read files.read.all sites.selected`
- Scopes single: `sites.read.all`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open SharePoint credential form. Select Delegated mode | Scopes field is visible |
| 2 | Inspect the Scopes input for placeholder or hint text | Hint text reads Enter scopes separated by commas or spaces or similar |
| 3 | Enter comma-separated scopes: `sites.read.all, user.read, files.read.all, sites.selected` | Field accepts the value without trimming or auto-correcting |
| 4 | Click Login | OAuth popup opens. The scope URL parameter in the popup URL contains all four scopes requested |
| 5 | Inspect the popup URL before completing. Verify the scope parameter | scope=sites.read.all user.read files.read.all sites.selected or equivalent in the redirect URL |
| 6 | Enter a single scope `sites.read.all` and click Login | OAuth popup opens requesting only sites.read.all scope |

## Expected Final State

OAuth popup opens requesting only sites.read.all scope

## Pass/Fail Criteria

**Pass:**
- Both comma and space-separated scopes are accepted
- All scopes are passed to the OAuth authorization URL
- Hint text is visible in the Scopes field
- Single scope works as well as multiple

**Fail:**
- Only one separator format is accepted
- Scopes are truncated or only first scope is passed
- Hint text is absent
- Field validation rejects valid scope strings

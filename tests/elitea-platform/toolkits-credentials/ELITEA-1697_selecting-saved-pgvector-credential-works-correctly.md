---
id: ELITEA-1697
title: Verify selecting an existing saved PGVector credential from dropdown works correctly
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1697: Verify selecting an existing saved PGVector credential from dropdown works correctly

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting a saved PGVector credential from the toolkit dropdown works correctly, the selection persists after saving, and is properly indicated with a checkmark.

## Preconditions

- User is logged in to `{{base_url}}`
- At least 2 saved PGVector credentials exist
- User is on agent/toolkit configuration page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Credential | elitea-pgvector |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent configuration page | Agent configuration page loads |
| 2 | Expand "Toolkit" section | Toolkit section expands |
| 3 | Click on "Pgvector Configuration" dropdown | Dropdown opens with credentials list |
| 4 | Click on a saved PGVector credential (e.g., "elitea-pgvector") | Dropdown closes; selected credential name appears in the PGVector Configuration field |
| 5 | Click "Save" button to save agent configuration | Agent configuration saves successfully with success message |
| 6 | Close the agent configuration page | Agent closes |
| 7 | Reopen the same agent | Agent configuration reopens |
| 8 | Expand "Toolkit" section and check PGVector Configuration field | Selected credential "elitea-pgvector" is still displayed |
| 9 | Open PGVector dropdown again | Checkmark appears next to the saved credential |

## Expected Final State

Selected PGVector credential persists across save/reload cycles and is clearly marked with a checkmark in the dropdown.

## Pass/Fail Criteria

**Pass:**
- Credential selection works smoothly
- Selected credential displays in the field after selection
- Configuration saves successfully
- Selection persists after reopening agent
- Checkmark appears next to selected credential
- No JavaScript errors in console

**Fail:**
- Selection doesn't work or dropdown doesn't close
- Selected credential doesn't persist after save
- Checkmark doesn't appear
- JavaScript errors occur during selection

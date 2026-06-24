---
id: ELITEA-1713
title: Verify ability to edit existing PGVector credentials from Settings
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one PGVector credential exists (e.g., "elitea-pgvector")
- User has permissions to edit integrations

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Existing Credential | elitea-pgvector |
| New Port Value | [different valid port] |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | Page loads |
| 2 | Locate existing PGVector credential "elitea-pgvector" in the list | Credential is visible |
| 3 | Click "Edit" icon/button for the credential | Edit form opens with all existing values pre-filled |
| 4 | Verify all fields are editable | All fields can be modified |
| 5 | Modify Port field to a different value | New value is accepted |
| 6 | Click "Save" button | Form submits; success message appears |
| 7 | Reopen the credential to verify changes | Edit form opens with updated Port value |

## Expected Final State

PGVector credentials can be edited successfully with changes persisting correctly.

## Pass/Fail Criteria

**Pass:**
- Edit form opens with pre-filled values
- All fields are editable
- Modified values can be saved successfully
- Success message appears after save
- Changes persist when credential is reopened
- No data loss during edit
- No JavaScript errors in console

**Fail:**
- Edit form doesn't open or is incomplete
- Fields are not editable
- Save fails with error
- Changes don't persist
- Data loss occurs
- JavaScript errors occur

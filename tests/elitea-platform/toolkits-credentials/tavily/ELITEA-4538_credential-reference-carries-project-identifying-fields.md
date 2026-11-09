---
id: ELITEA-4538
title: "Verify the credential reference carries project/configuration identifying fields in the toolkit form's payload"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- Browser developer tools (Network tab or page inspection) available

## Test Data

| Field | Value |
|-------|-------|
| Credential | A credential from the current project |
| Shared credential (if available) | A credential from a different project |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open or create a Tavily toolkit and select a credential from the current project | Credential is selected |
| 2 | Using developer tools, inspect the underlying form payload/hidden field for the selected credential reference | Includes `configuration_uuid` and `configuration_project_id` matching the current project's ID, plus a private/shared flag |
| 3 | If a shared credential from a different project is selectable, repeat | `configuration_project_id` reflects that other project's ID, not the current one |

## Expected Final State

The credential reference is confirmed to carry correct identifying fields for server-side provenance.

## Pass/Fail Criteria

**Pass:**
- `configuration_uuid` and `configuration_project_id` are present and correct for both same-project and cross-project credentials

**Fail:**
- Either field is missing or incorrect

---
id: ELITEA-4651
title: "Deleting Credentials preserves underlying Secrets and surfaces dependent errors"
priority: high
type: integration
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- A Credential built from a project Secret, used by a Toolkit/Agent/Pipeline

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Secret | QA-Secret-1 |
| Credential built from Secret | QA-Credential-1 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the current state of the related Secret in Settings → Secrets before deletion | Secret present with expected value/reference |
| 2 | Select Credentials in Delete Project Data and complete the deletion | Deletion completes |
| 3 | Check Settings → Secrets | Underlying Secret entry still present, not deleted |
| 4 | Open the Agent/Pipeline/Toolkit that referenced the deleted Credential | Shows the standard missing-credential error/warning state, consistent with existing credential-error UI |

## Expected Final State

Secrets are untouched by Credentials deletion; dependents show the standard, already-existing error handling.

## Pass/Fail Criteria

**Pass:**
- Secret preserved; dependent shows standard error state

**Fail:**
- Secret is deleted, or dependent shows an unhandled/broken state instead of the standard error UI

---
id: ELITEA-4640
title: "Deleting in-use Toolkits or Credentials proceeds without blocking for unpublished dependents"
priority: critical
type: integration
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- An unpublished Agent or Pipeline configured with a Toolkit that uses a Credential, both present in the target project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent/Pipeline | Unpublished test Agent "QA-Dependent-Agent" |
| Toolkit | Toolkit attached to QA-Dependent-Agent |
| Credential | Credential used by that Toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent/Pipeline and confirm its Toolkit is attached and Credential is valid | No error banner shown |
| 2 | In Delete Project Data, select Credentials (and/or Toolkits), complete the typed-DELETE confirmation flow | No warning step blocks or interrupts deletion due to in-use status |
| 3 | Confirm deletion completes | Deletion reports success |
| 4 | Reopen the Agent/Pipeline | Standard missing-credential/missing-toolkit error state shown, not a crash or blank/corrupted configuration |

## Expected Final State

The Credential/Toolkit is deleted; the dependent unpublished Agent/Pipeline shows the standard missing-dependency error state.

## Pass/Fail Criteria

**Pass:**
- Deletion is not blocked solely because the item is in use by an unpublished entity
- Dependent entity shows the standard error state afterward

**Fail:**
- Deletion is blocked due to ordinary in-use status
- Dependent entity crashes or shows a corrupted/blank configuration

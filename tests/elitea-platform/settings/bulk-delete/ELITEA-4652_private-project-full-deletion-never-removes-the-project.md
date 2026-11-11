---
id: ELITEA-4652
title: "Private project full-type deletion never removes the project itself"
priority: medium
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Private project owned by the test user

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As owner, click "Select all" in Delete Project Data and complete the deletion for all available types | Deletion completes |
| 2 | Confirm the project itself still exists and is accessible (name, icon, Settings → General all load normally) | Project fully intact and accessible |
| 3 | Check project-level settings (AI Configurations, Default Modules) | Values unaffected and unchanged from before deletion |

## Expected Final State

The project and its non-targeted settings remain fully intact after a full-type deletion.

## Pass/Fail Criteria

**Pass:**
- Project and its settings survive unchanged

**Fail:**
- Project itself is removed/inaccessible, or unrelated settings are altered

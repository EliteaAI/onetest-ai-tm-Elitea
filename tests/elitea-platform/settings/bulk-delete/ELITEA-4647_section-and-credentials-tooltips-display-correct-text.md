---
id: ELITEA-4647
title: "Section and Credentials info tooltips display correct text"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Hover/click the section-level info icon in Delete Project Data | Tooltip states deletion covers all project-owned items of selected types (not just the current user's own items), and that resources shared from other projects are not deleted |
| 2 | Hover/click the info icon next to Credentials | Tooltip states credentials, tokens, and other secrets are excluded from project backups and cannot be restored from them, and advises ensuring required credentials can be recreated before deleting |
| 3 | Review the section description/tooltip text for chats/attachments | UI communicates that chats and attachments can only be restored if included in a backup |

## Expected Final State

All three pieces of informational text are present and match the specified wording.

## Pass/Fail Criteria

**Pass:**
- All three texts present and correct

**Fail:**
- Any tooltip missing or text incorrect/misleading

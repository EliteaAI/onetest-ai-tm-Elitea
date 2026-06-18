---
id: ELITEA-0933
title: "Regression — Existing Chat Conversations Load Correctly After Context Changes"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, regression, story:3395, r-2.0.4, chat]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0933: Regression — Existing Chat Conversations Load Correctly After Context Changes

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that existing chat conversations created before Project Context was enabled continue to load correctly after context is enabled, changed, or disabled.

**Coverage:**
- Old conversations load correctly after context is enabled
- Old conversations unaffected by content changes
- Old conversations load correctly after context is disabled

## Preconditions

- At least 3 existing chat conversations present in the project, created before Project Context was configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm that several existing chat conversations are present in the sidebar (created before Project Context was configured). | Conversations visible in sidebar. |
| 2 | Enable Project Context and save content. | Toggle ON, content saved. |
| 3 | Open each existing conversation from the sidebar. | All conversations load correctly. All messages are intact. No errors or data loss. |
| 4 | Edit and save new Project Context content. | Existing conversations still load correctly after the content change. |
| 5 | Disable the Enable toggle. | Existing conversations still load correctly with toggle OFF. |

## Expected Final State

Existing conversations still load correctly with toggle OFF.

## Pass/Fail Criteria

**Pass:**
- All existing conversations load with messages intact
- No data loss or corruption after context changes

**Fail:**
- Existing conversations fail to load
- Messages missing or corrupted after enabling/changing context

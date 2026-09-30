---
id: ELITEA-3445
title: "Chat Templates: Save/Cancel and Unsaved Changes Handling"
priority: high
type: functional
module: settings-chat-configuration
status: draft
execution_type: manual
tags: [feat:settings, feat:chat-config, story:6724, regression, data-integrity]
requirements: [EliteaAI/elitea_issues#6800]
---
# ELITEA-3445: Chat Templates: Save/Cancel and Unsaved Changes Handling

**Module:** Settings → General → Chat Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify Save/Cancel buttons work correctly during template creation and editing, and unsaved-changes prompts prevent accidental loss of work — regression check for #6800 (Cancel should discard changes).

**Coverage:** Regression — [EliteaAI/elitea_issues#6800](https://github.com/EliteaAI/elitea_issues/issues/6800).

## Preconditions

- User is logged in as an Admin to a project
- Chat Configuration section is accessible in Settings → General
- At least one chat template exists (or follow steps starting from "New template")

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **+ New template** to create a new unsaved template. | Template editor opens with focused, selected name field; **Save** button is **disabled** (no changes yet). |
| 2 | Type a template name (e.g., "Test Template"). | **Save** button becomes **enabled** (name is a change). |
| 3 | Click **Cancel** without saving. | Editor closes; template is discarded; template list does not include "Test Template" (regression check for **#6800**). |
| 4 | Select an existing template and modify its name (e.g., "Old Name" → "New Name"). | **Save** button is **enabled**; Cancel button is available. |
| 5 | Click **Cancel** without saving the name change. | Name reverts to "Old Name"; editor keeps template selected but unsaved changes are discarded (regression check for **#6800**). |
| 6 | Modify the template name again. Without saving, click **+ New template** button. | Unsaved-changes prompt appears: "You have unsaved changes in this template. Discard them?" with Cancel and Discard buttons. |
| 7 | Click **Cancel** in the prompt. | Prompt closes; editor returns to the previously edited template with changes still present; **Save** button remains enabled. |
| 8 | Click **Discard** in the prompt. | Prompt closes; new template editor opens; unsaved changes from the prior template are lost. |
| 9 | Modify a template and click another template in the list without saving. | Same unsaved-changes prompt appears as step 6. Discard → new template loads with clean state. |
| 10 | Save a template successfully. | **Save** button becomes **disabled**. Make another change (e.g., name again). | **Save** button re-enables. |

## Expected Final State

- **Save** button is disabled until a change is made; disabled after a successful save.
- **Cancel** during creation discards the unsaved template entirely (regression check for #6800).
- **Cancel** during editing discards unsaved changes, preserving the prior saved state (regression check for #6800).
- Switching templates or creating a new one with unsaved changes triggers a confirmation prompt; Discard loses changes, Cancel keeps them.

## Pass/Fail Criteria

**Pass:**
- Steps 3 and 5: Cancel successfully discards all changes (regression: #6800)
- Save button state (enabled/disabled) matches expected conditions
- Unsaved-changes prompt appears correctly and both options work as expected
- After discard, template loads with clean prior saved state

**Fail:**
- Cancel does not discard changes (regression of #6800)
- Unsaved-changes prompt missing or non-functional
- Save/Cancel buttons behave inconsistently or don't match spec

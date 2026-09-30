---
id: ELITEA-3447
title: "Chat Templates: 5-Template Limit and Mid-Turn Input Toggle"
priority: medium
type: functional
module: settings-chat-configuration
status: draft
execution_type: manual
tags: [feat:settings, feat:chat-config, story:6724]
requirements: [EliteaAI/elitea_issues#6724]
---
# ELITEA-3447: Chat Templates: 5-Template Limit and Mid-Turn Input Toggle

**Module:** Settings → General → Chat Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the maximum 5-template limit is enforced, the "New template" button state changes correctly, and the Mid-turn input toggle is present, functional, and project-level (not per-template).

**Coverage:** [EliteaAI/elitea_issues#6724](https://github.com/EliteaAI/elitea_issues/issues/6724).

## Preconditions

- User is logged in as an Admin to a project
- Chat Configuration section is accessible in Settings → General

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create templates until 5 exist (or delete existing templates to reach 5). Counter shows `5 of 5`. | **"New template"** button still visible but changes to show **"Template limit reached (5 of 5)"** text and is non-interactive (`aria-disabled="true"`). Tooltip reads: "You can have up to 5 templates. Delete one to add another." |
| 2 | Attempt to click the disabled button. | No action; button is non-interactive; no template is created. |
| 3 | Delete one template. Counter now shows `4 of 5`. | **"New template"** button returns to interactive state showing **"+ New template"** and full text (not grayed out). Button is clickable again. |
| 4 | Scroll down to find the **Mid-turn input** toggle section. | Section is visible inside Chat Configuration (not in a separate CHAT section). Title reads **"Mid-turn input"** (no "(Beta)" wording). Description: "Send a message to an agent while it is still working, to steer the rest of the run." |
| 5 | Toggle the Mid-turn input switch to the **on** position. | Toggle switches on; **Save** is **not** required (saves immediately, project-level). Verify no Save button needed for this toggle. |
| 6 | Create a new chat and verify the toggle state is reflected (agent is running, mid-turn input is available/unavailable based on step 5). | Toggle state is applied project-wide; all new chats in this project respect it. |
| 7 | Open a different template (without changing Mid-turn input). Verify the toggle position is **the same across all templates** (not per-template). | Toggle state is consistent; switching templates does **not** change the toggle position. It is project-level, not per-template. |

## Expected Final State

- **5-template limit** is enforced; "New template" button is disabled at 5 templates with appropriate tooltip/text.
- **Mid-turn input** toggle is inside Chat Configuration, without "(Beta)" wording, saves immediately without a Save button, and is project-level (not per-template).

## Pass/Fail Criteria

**Pass:**
- At 5 templates, "New template" button is disabled with correct tooltip
- Deleting a template re-enables the button
- Mid-turn input toggle is present without "(Beta)"
- Toggle saves immediately, not requiring a Save button
- Toggle state is consistent across all templates (project-level)

**Fail:**
- Button still clickable at 5 templates
- New template created at limit
- Mid-turn input shows "(Beta)" wording
- Toggle requires a Save button to apply
- Toggle state changes per-template

---
id: ELITEA-3976
title: "Clarifying question UI and resulting chips remain visually stable across question types with no styling issues"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, ui, styling, clarifying-question-ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3976: Clarifying question UI and resulting chips remain visually stable across question types with no styling issues

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder, Project Context Builder, and Ask User are enabled

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Step through a clarification flow containing a single-select, a multi-select, and a free-text question | Each question type renders with consistent layout, spacing, and styling; no overlapping or clipped elements |
| 2 | Inspect the resulting Skill chip and Project Context chip in the chat response | Chip labels are not truncated or misaligned, and styling is consistent with other chips/links in the chat UI |

## Expected Final State

No cosmetic/styling defects are observed across clarifying-question types or the resulting entity chips.

## Pass/Fail Criteria

**Pass:**
- All question types render with consistent styling
- Chips display without truncation or misalignment

**Fail:**
- Any visible styling defect, truncation, or misalignment is observed

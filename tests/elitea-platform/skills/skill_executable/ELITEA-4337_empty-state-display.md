---
id: ELITEA-4337
title: "Verify empty state displays when no skill runs exist in history"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill exists with NO run history (newly created or all history deleted)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Skill Name | [New skill with no runs] |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill OR navigate to a skill with no run history | Skill is accessible |
| 2 | Navigate to the Run History page | Run History page loads |
| 3 | Observe the page content | Empty state message or illustration displays |
| 4 | Verify empty state provides helpful guidance | Message explains how to run the skill or why history is empty |
| 5 | Check for any action buttons (e.g., "Run Skill" button) | Action buttons are present if applicable |
| 6 | Verify no table or list is displayed | No empty table rows or broken table structure appears |
| 7 | Run the skill once | Skill executes successfully |
| 8 | Return to Run History page | The new run appears in the table; empty state is gone |

## Expected Final State

When no runs exist, an informative empty state displays with guidance on how to create the first run. After the first run, the table replaces the empty state.

## Pass/Fail Criteria

**Pass:**
- Empty state displays when no runs exist
- Message is clear and helpful
- No broken table structure appears
- After first run, history table displays correctly

**Fail:**
- Empty state is missing or shows error
- Message is unclear or missing
- Broken table structure displays
- After first run, history does not update

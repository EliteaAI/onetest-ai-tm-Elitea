---
id: ELITEA-4649
title: "Completion reports accurate success/partial-failure outcome and refreshes counts"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Ability to induce a partial failure for at least one item (e.g., item locked/in-use), if feasible in the test environment

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select one or more types with a normal, fully deletable set of items, and submit the deletion | Deletion completes |
| 2 | Review the completion report | Reports a success outcome with the correct deleted count per type |
| 3 | Check the checkbox counts in Delete Project Data without reloading the page | Counts update to reflect the new (lower) values automatically |
| 4 | Navigate to the corresponding list (e.g., Chats list) | List reflects the updated contents |
| 5 | If a partial-failure scenario can be induced, repeat steps 1–2 under that condition | Report shows both deleted count and failed count accurately, not a blanket success or failure |

## Expected Final State

The UI's reported outcome and refreshed counts are always accurate, including under partial failure.

## Pass/Fail Criteria

**Pass:**
- Reported outcome and refreshed counts match actual results in all cases

**Fail:**
- Outcome misreported, or counts/lists require a manual refresh to update

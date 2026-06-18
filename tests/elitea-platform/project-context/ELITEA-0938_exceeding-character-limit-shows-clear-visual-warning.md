---
id: ELITEA-0938
title: "Exceeding Character Limit Shows Clear Visual Warning"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, char-limit, story:3395, usability, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395, EliteaAI/elitea_issues#5309]
---
# ELITEA-0938: Exceeding Character Limit Shows Clear Visual Warning

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the character counter shows a clear visual warning (red styling + message) when the 2500-character limit is reached.

**Coverage:**
- Counter changes styling at limit
- Warning message is shown
- Behavior consistent with other limited fields in the app

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Project Context editor. Type until the counter shows '0 characters left'. | Counter is visible showing 0. |
| 2 | Observe the counter's visual styling at 0 chars. | Counter turns red (or equivalent warning color/style). |
| 3 | Check for a warning message near the counter. | A message such as 'You have reached the maximum character limit' is clearly visible. |
| 4 | Paste additional text beyond the limit. | Counter stays at 0; warning remains; input is truncated at the boundary. |
| 5 | Compare counter behavior with another limited text field in the app (e.g. welcome message field). | Behavior is consistent — same red styling and limit message used in other fields. |

## Expected Final State

Behavior is consistent — same red styling and limit message used in other fields.

## Pass/Fail Criteria

**Pass:**
- Counter turns red (or equivalent) at 0 chars left
- Warning message is clearly visible
- Behavior matches other limited fields

**Fail:**
- Counter stays neutral (no red/warning) at the limit
- No message shown when limit reached
- User has no indication that content was truncated

---
id: ELITEA-3424
title: "System State Variables tool_outcomes/last_tool_outcome Toggle Is OFF by Default"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, state-variables, story:6593, reserved-variables, regression]
requirements: [EliteaAI/elitea_issues#6593]
---
# ELITEA-3424: System State Variables Toggle Is OFF by Default

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Confirm the enable/disable toggle on the `tool_outcomes` and `last_tool_outcome` system rows is OFF the first time each row appears, per both the original AC and the reporter's follow-up comment ("...with a turned-off toggle by default").

**Coverage:** AC / regression — the merged UI (`EliteaUI#1041`) passes `enabled` as a bare, hardcoded JSX boolean (`enabled` → `enabled={true}`) for every system row, with no logic reading a persisted default-off state.

## Preconditions

- User has permission to create pipelines in the current project
- A pipeline exists (new, or one where the two system rows are already visible per [[ELITEA-3423]])

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the STATE panel on a pipeline where `tool_outcomes` and `last_tool_outcome` rows are visible, before interacting with either toggle. | Both rows are visible. |
| 2 | Inspect the toggle/switch control on the `tool_outcomes` row. | Toggle is in the OFF position. |
| 3 | Inspect the toggle/switch control on the `last_tool_outcome` row. | Toggle is in the OFF position. |
| 4 | Reload the page and reopen the STATE panel on the same pipeline. | Both toggles remain OFF (default state persists across a fresh load, not just the initial render). |

## Expected Final State

Both system rows load with their toggle OFF until a user explicitly turns either one on.

## Pass/Fail Criteria

**Pass:**
- Steps 2–4 all show the toggle OFF

**Fail:**
- Either toggle shows ON on first appearance (current implementation hardcodes `enabled={true}` unconditionally) — file as a gap against #6593's AC and the reporter's own clarifying comment

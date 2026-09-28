---
id: ELITEA-3433
title: "Deleting a Preconfigured Participant From a Live Chat Works on the First Attempt"
priority: medium
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, story:6358, default-chat-config, regression]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3433: Deleting a Preconfigured Participant From a Live Chat Works on the First Attempt

**Module:** Chat · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm deleting a preconfigured participant from an individual chat's participant panel removes it immediately and it does not reappear — regression coverage for two independently-fixed bugs (an async state-sync race and a portal event-bubbling re-selection).

**Coverage:** Regression — `EliteaUI#1077`.

## Preconditions

- A project with 2+ preconfigured participants configured
- A manually-addable participant also available (not in the preconfigured list)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new chat with preconfigured participants pre-populated. | Preconfigured participants appear in the panel. |
| 2 | Delete one preconfigured participant via its delete control. | It is removed on the **first click** and does not reappear afterward. |
| 3 | Delete a second, different preconfigured participant in the same chat. | Same result — removed on the first click, no reappearance. |
| 4 | Manually add a participant not from the preconfigured list, then delete it. | It deletes correctly and independently of the preconfigured-participant deletions above. |

## Expected Final State

Deleting any preconfigured participant from a live chat works correctly on the first attempt, every time, and does not interfere with deleting manually-added participants.

## Pass/Fail Criteria

**Pass:**
- All deletions in steps 2–4 succeed on the first attempt with no reappearance

**Fail:**
- A deleted participant reappears after deletion (either bug: stale-ref race or bubbled re-selection)

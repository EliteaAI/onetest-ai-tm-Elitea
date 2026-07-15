---
id: ELITEA-1793
title: "Skills from a removed Agent participant are not shown via `~` in Chat"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: automation.tests.ui.skills.test_ghost_skill_after_agent_removed.TestGhostSkillAfterAgentRemoved.test_ghost_skill_not_shown_after_agent_participant_removed
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/284
---

# ELITEA-1793: Skills from a removed Agent participant are not shown via `~` in Chat

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that when an Agent participant is removed from a Chat conversation, the Skills that were brought in by that Agent are no longer available via the `~` mention trigger in the Chat input.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills, Agents, and Chat sections are available in the project.
- An Agent ("Joker Agent") exists with at least one Skill attached ("Robot-Joker").
- A Chat conversation exists or can be created.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | "Joker Agent" |
| Skill attached to Agent | "Robot-Joker" |
| Chat conversation | (new or existing conversation) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Chat conversation and add "Joker Agent" as a participant | "Joker Agent" appears in the conversation participants list |
| 2 | In the Chat input field, type `~` | A suggestion dropdown appears showing "Robot-Joker" (the Skill from "Joker Agent") |
| 3 | Dismiss the suggestion dropdown without selecting anything | Dropdown is closed |
| 4 | Remove "Joker Agent" from the conversation participants | "Joker Agent" is no longer listed as a participant |
| 5 | In the Chat input field, type `~` again | A suggestion dropdown either does not appear, or appears without "Robot-Joker" listed |
| 6 | Confirm "Robot-Joker" is absent from the `~` suggestion list | "Robot-Joker" is not shown in the suggestions |

---

## Expected Final State

After removing the Agent participant, the Skills associated with that Agent are no longer surfaced through the `~` mention trigger in the Chat input. No ghost Skill references remain accessible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Before removal, "Robot-Joker" is visible in `~` suggestions.
- After removal, "Robot-Joker" is not shown in `~` suggestions.

**Fail:**
- Any step produces an error or unexpected result.
- "Robot-Joker" still appears in `~` suggestions after the Agent is removed from the conversation.

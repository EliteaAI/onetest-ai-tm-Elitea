---
id: ELITEA-1791
title: "`~` mention in Agent instructions lists only currently attached Skills"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_agent_instructions_tilde_mention.TestTildeMentionListsOnlyAttachedSkills.test_tilde_mention_in_instructions_lists_only_attached_skills
---

# ELITEA-1791: `~` mention in Agent instructions lists only currently attached Skills

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that when a user types `~` in the Agent instructions editor, the autocomplete or suggestion list shows only the Skills currently attached to that Agent, not all Skills in the project.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- At least 3 Skills exist in the project.
- An Agent exists with only some of those Skills attached (e.g., 2 out of 3).

---

## Test Data

| Field | Value |
|-------|-------|
| Total Skills in project | 3 (e.g., "Skill A", "Skill B", "Skill C") |
| Skills attached to Agent | "Skill A", "Skill B" |
| Skills NOT attached to Agent | "Skill C" |
| Trigger character | `~` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent in edit mode that has "Skill A" and "Skill B" attached | Agent edit form is open with 2 Skills attached |
| 2 | Navigate to the Agent instructions field | Instructions text area is focused and editable |
| 3 | Type `~` in the instructions field | A suggestion/autocomplete dropdown appears |
| 4 | Inspect the list of suggestions shown | Only "Skill A" and "Skill B" are listed; "Skill C" is NOT shown |
| 5 | Select "Skill A" from the suggestions | `~Skill A` (or the appropriate reference syntax) is inserted into the instructions |
| 6 | Type `~` again after removing Skill A reference | Suggestion list appears again with only the attached Skills |

---

## Expected Final State

The `~` mention autocomplete in Agent instructions is scoped to only the currently attached Skills. Skills that exist in the project but are not attached to the Agent are not surfaced.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- `~` trigger shows only "Skill A" and "Skill B" in suggestions.
- "Skill C" does not appear in the suggestion list.

**Fail:**
- Any step produces an error or unexpected result.
- The suggestion list shows Skills not attached to the Agent.
- No suggestion list appears when `~` is typed.

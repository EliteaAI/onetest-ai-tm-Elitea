---
id: ELITEA-1900
title: "Agent name character limit enforced at 32 characters"
priority: low
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_name_character_limit.test_agent_name_truncated_at_32_characters
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1292
---

# ELITEA-1900: Agent name character limit enforced at 32 characters

**Module:** agents · **Priority:** low · **Type:** functional

**Objective:** Verify that the Name field on the Create Agent page enforces a 32-character maximum, truncating longer input and not showing an error when the name is exactly at the limit.

---

## Preconditions

- User is logged in to the Elitea platform.
- The Create Agent page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Input text | 80-character string (e.g., "A" repeated 80 times) |
| Max allowed length | 32 characters |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Create Agent page | The Create Agent form is displayed |
| 2 | Type 80 characters into the Name field | Input is entered in the Name field |
| 3 | Verify the input is truncated to a maximum of 32 characters (no more can be entered) | The Name field contains exactly 32 characters; no additional input is accepted |
| 4 | Verify no error state is shown when the name is exactly at the 32-char limit | No error message or visual error state is displayed |
| 5 | Verify the Save button is enabled (Description also filled) | Save button is enabled when both Name (32 chars) and Description are filled |

---

## Expected Final State

The Name field contains exactly 32 characters with no error state, and the Save button is enabled when Description is also filled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Name field is truncated at 32 characters, no error shown at limit, Save button enabled.

**Fail:**
- Any step produces an error or unexpected result.
- Input beyond 32 characters is accepted, an error appears at the limit, or Save is disabled despite both fields being filled.

---
id: ELITEA-1883
title: "Add two variables and verify they persist after reload"
priority: low
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_add_variables_persist_after_reload.TestAgentAddVariablesPersistAfterReload.test_add_two_variables_and_verify_they_persist_after_reload
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/564
---

# ELITEA-1883: Add two variables and verify they persist after reload

**Module:** agents · **Priority:** low · **Type:** functional

**Objective:** Verify that variables referenced in the Instructions field auto-populate in the Variables section, that values can be entered and saved, and that both variables with their values persist after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Instructions text | {{MY_VAR}} and {{API_URL}} |
| MY_VAR value | hello_world |
| API_URL value | https://example.com |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Switch the Instructions section to Edit mode (click the "Edit mode" toggle; it opens in Preview mode), then in the Instructions field, type "{{MY_VAR}} and {{API_URL}}" | The text is entered in the Instructions field |
| 3 | Verify the Variables section appears automatically with "MY_VAR" and "API_URL" listed | The Variables section is displayed with both variable names as rows |
| 4 | Enter value "hello_world" for MY_VAR | MY_VAR field shows "hello_world" |
| 5 | Enter value "https://example.com" for API_URL | API_URL field shows "https://example.com" |
| 6 | Click Save | Save completes successfully |
| 7 | Reload the page | The page reloads |
| 8 | Verify both MY_VAR and API_URL appear in the Variables section with their correct values | Both variables are listed with "hello_world" and "https://example.com" respectively |

---

## Expected Final State

After reload, both MY_VAR (value: hello_world) and API_URL (value: https://example.com) are present in the Variables section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both variables appear with their correct values after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- Variables are missing, values are wrong, or the Variables section does not appear automatically.

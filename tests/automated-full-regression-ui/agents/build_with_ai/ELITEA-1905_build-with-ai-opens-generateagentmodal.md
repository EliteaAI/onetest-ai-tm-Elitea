---
id: ELITEA-1905
title: "Build with AI opens GenerateAgentModal"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1905: Build with AI opens GenerateAgentModal

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the Magic Wand (Build with AI) button on the New Agent creation page opens the GenerateAgentModal with all required UI elements present.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The New Agent creation page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as admin or editor and navigate to New Agent creation | The New Agent creation page is displayed with Build with AI button |
| 2 | Click the Build with AI button in the tab bar | The Build with AI modal opens |
| 3 | Verify the modal contains a natural-language prompt input field | A text input field for entering a natural-language description is present in the modal |
| 4 | Verify the modal contains a "Generate Draft" button | The "Generate Draft" button is visible and disabled |
| 5 | Verify the modal contains a Cancel button | The Cancel button is visible in the modal |

---

## Expected Final State

The GenerateAgentModal is open and displays: a prompt input field, a "Generate agent" button, and a Cancel button.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The GenerateAgentModal opens and contains the prompt input, "Generate agent" button, and Cancel button.

**Fail:**
- Any step produces an error or unexpected result.
- The modal does not open, or any required UI element is missing.

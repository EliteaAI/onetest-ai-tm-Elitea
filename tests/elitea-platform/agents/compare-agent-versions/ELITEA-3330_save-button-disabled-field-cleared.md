---
id: ELITEA-3330
title: "Save button becomes disabled when Conversation Starter field is cleared in Agent comparison modal"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, bug:6564]
requirements: [EliteaAI/elitea_issues#6304, EliteaAI/elitea_issues#6564]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions containing Conversation Starters

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version 1 Chat Starter 1 | "How can I get started with this tool?" |
| Version 1 Chat Starter 2 | "What features are available?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Navigate to User Interaction section | Section loads with Chat Starters |
| 3 | Verify Save button for Version 1 is initially enabled (with valid data present) | Save button is enabled and clickable |
| 4 | Locate first Conversation Starter field in Version 1 column | Field displays "How can I get started with this tool?" |
| 5 | Select all text in the field and delete it (clear the field completely) | Field is now empty |
| 6 | Verify Save button for Version 1 becomes **disabled** immediately after clearing | Save button is disabled (grayed out, not clickable) |
| 7 | Attempt to click the disabled Save button | Button does not respond, no save operation occurs |
| 8 | Verify NO ValueError message appears (save is prevented by disabled button) | No error message displayed |
| 9 | Re-enter text in the Conversation Starter field: "How do I begin?" | Field contains valid text |
| 10 | Verify Save button for Version 1 becomes **enabled** again | Save button is enabled and clickable |
| 11 | Click Save button | Save operation executes successfully |
| 12 | Verify changes are saved without errors | Success message appears, no ValueError |

## Expected Final State

Save button becomes disabled when Conversation Starter field is cleared, preventing invalid save attempts. Button re-enables when valid text is entered.

## Pass/Fail Criteria

**Pass:**
- Save button is initially enabled with valid data
- Save button becomes disabled immediately after clearing Conversation Starter field
- Disabled Save button is not clickable
- No ValueError appears (save prevented by validation)
- Save button re-enables when valid text is entered

**Fail:**
- Save button remains enabled when field is cleared
- ValueError appears after clicking Save on cleared field
- Save button does not re-enable after entering valid text

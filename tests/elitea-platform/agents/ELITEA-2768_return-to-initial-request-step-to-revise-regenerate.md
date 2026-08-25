---
id: ELITEA-2768
title: "User can return to initial request step to revise and regenerate"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent's configuration page is open

## Test Data

| Field | Value |
|-------|-------|
| Initial prompt | "Improve the instructions" |
| Revised prompt | "Improve the instructions and add error handling" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and initiate Edit with AI | Modal opens at prompt entry step |
| 2 | Enter the initial prompt "Improve the instructions" | Prompt accepted |
| 3 | Generate the draft and navigate to a wizard step | Suggestions based on the initial prompt shown |
| 4 | Click "Back to Enter request step" action | Modal returns to the prompt entry step |
| 5 | Verify the previous prompt text is preserved in the input field | Input shows "Improve the instructions" |
| 6 | Modify the prompt to "Improve the instructions and add error handling" | Input field updated with the revised text |
| 7 | Click "Generate Draft" again | Generation runs again |
| 8 | Verify new suggestions are generated based on the revised prompt | Instructions step shows a suggestion reflecting error-handling content, distinct from the earlier draft |

## Expected Final State

The user successfully revised the prompt from the entry step and obtained a new draft reflecting the revised instructions, without needing to reopen the modal from scratch.

## Pass/Fail Criteria

**Pass:**
- The prior prompt is preserved when returning to the entry step, and regeneration produces suggestions matching the revised prompt

**Fail:**
- The prompt input is cleared on return, or regeneration does not reflect the revision (e.g. identical to the first draft or fails)

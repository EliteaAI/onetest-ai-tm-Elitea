---
id: ELITEA-2494
title: "Same personality with different instructions in multiple conversations"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2494: Same personality with different instructions in multiple conversations

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify same personality can have conversation-specific instruction overrides

## Preconditions

- Settings has "QA" personality with instructions: "Be technical and testing-focused"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation A | |
| 2 | Open Context Management, turn ON | |
| 3 | Modify instructions to: "Be technical and focus on security testing" | |
| 4 | Save and send message: "Explain input validation" | |
| 5 | Observe security-focused response | |
| 6 | Create conversation B | |
| 7 | Open Context Management | |
| 8 | Verify personality is "QA" with original instructions | |
| 9 | Send message: "Explain input validation" | |
| 10 | Observe general testing-focused response | |

## Expected Results

- Conversation A has modified QA instructions (security focus)
- Conversation B has original QA instructions (general testing)
- Same personality can have different instruction overrides per conversation

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur

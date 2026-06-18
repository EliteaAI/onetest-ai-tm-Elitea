---
id: ELITEA-0544
title: "Cancel after modifying text — discards changes, restores original"
priority: critical
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0544: Cancel after modifying text — discards changes, restores original

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Cancel after editing discards all changes and does not trigger regeneration.

**Coverage:**
- Modified content is discarded
- Original message restored in read-only view
- No LLM regeneration triggered

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with a last user message and corresponding LLM response

## Test Data

- Original message: "What is machine learning?"
- Modified text (not submitted): "What is deep learning?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click Edit on the last user message ("What is machine learning?"). | Edit mode opens with original content pre-loaded. |
| 2 | Modify the text to "What is deep learning?" (do NOT click Save and apply). | The editable field now shows the modified text. |
| 3 | Click "Cancel". | Edit mode closes. The message reverts to read-only view showing "What is machine learning?" (the original). |
| 4 | Verify the LLM response below. | The LLM response remains the same as before editing. No new response was generated. No loading indicator appeared. |

## Expected Final State

The LLM response remains the same as before editing. No new response was generated. No loading indicator appeared.

## Pass/Fail Criteria

**Pass:**
- Original message content is fully restored after Cancel
- No regeneration occurs
- Conversation state is unchanged

**Fail:**
- Modified text persists after Cancel
- LLM response is regenerated
- Edit mode remains open

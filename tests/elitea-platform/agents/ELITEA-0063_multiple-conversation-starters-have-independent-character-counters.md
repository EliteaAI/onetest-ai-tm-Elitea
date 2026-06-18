---
id: ELITEA-0063
title: "Multiple Conversation Starters Have Independent Character Counters"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [meta:reported-by-support, nfr:validation, nfr:usability, eng:frontend, feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4963]
---
# ELITEA-0063: Multiple Conversation Starters Have Independent Character Counters

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that multiple Conversation Starters have independent character counters in collapsed mode

## Preconditions

- Logged in to {{base_url}}
- Existing agent open in edit mode

## Test Data

- BV1: 768-character string — exactly at the character limit
- BV2: 769-character string — one over the character limit (input truncated at 768)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click "Add" button to add first conversation starter. Type text in the first conversation starter field (e.g., "Hello, how can I help you today?") | Character counter appears below the field showing remaining characters (e.g., "741 characters left") |
| 2 | Click "Add" button to add second conversation starter. Type different length text in the second conversation starter field (e.g., "Hi"). | Second field has its own character counter with different value than the first (e.g., "766 characters left"). |
| 3 | Verify both counters are visible simultaneously | Each conversation starter field displays its own independent counter reflecting the actual text length in that specific field. |

## Expected Final State

Each conversation starter field displays its own independent counter reflecting the actual text length in that specific field.

## Pass/Fail Criteria

**Pass:**
- Character counters are independent per field — typing in one starter does not affect the counter of another.

**Fail:**
- Characters that are left add up
- Only one starter is visible

---
id: ELITEA-2210
title: "Chat – Tool Output Rendering – Verify Tool Execution Results Display as Chips When Toolkit Called Directly"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2210: Chat – Tool Output Rendering – Verify Tool Execution Results Display as Chips When Toolkit Called Directly

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that tool execution results appear as chips above the LLM response when a toolkit is called directly.

---

## Preconditions

- User is logged in to the Elitea platform.
- A toolkit (e.g. 'aaa' with delete_file tool) is added as participant.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | use delete_file toolkit to remove from the bucket all files |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Add toolkit 'aaa' via + > Toolkits (no agent) | Toolkit in PARTICIPANTS |
| 2 | Send 'use delete_file toolkit to remove from the bucket all files' | LLM processes; 'Thought for X secs' appears |
| 3 | Wait for tool execution to complete | LLM response appears |
| 4 | Verify chips at top of response: LLM model chip (e.g. 'Anthropic Claude 4.5 Sonnet') and toolkit tool chip (e.g. 'aaa: delete_file') | Both chips shown horizontally |
| 5 | Verify each chip has appropriate icon and label | Icons and labels correct |

---

## Expected Final State

Tool execution chips shown above LLM response.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Tool execution chips displayed correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Chips missing or incorrectly labeled.

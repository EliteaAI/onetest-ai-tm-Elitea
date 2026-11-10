---
id: ELITEA-2206
title: "Chat – Mentions with # – Verify Typing # Displays All Available Agents and Pipelines"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2206: Chat – Mentions with # – Verify Typing # Displays All Available Agents and Pipelines

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that typing '#' in the message input shows a 'SEARCH RESULTS' dropdown with all available agents and pipelines.

---

## Preconditions

- User is logged in to the Elitea platform.
- Agents and pipelines exist in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open a conversation and type '#' in the message input | 'SEARCH RESULTS' dropdown appears |
| 2 | Verify agents shown with 'Agent' subtitle and agent icons | Agent items visible |
| 3 | Verify pipelines shown with 'Pipeline' subtitle and pipeline icons | Pipeline items visible |
| 4 | Verify list includes agents from current project and Catalog | All sources represented |
| 5 | Press elsewhere to close dropdown | Dropdown closes |

---

## Expected Final State

'#' shows all available agents and pipelines from all sources.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- '#' dropdown shows agents and pipelines.

**Fail:**
- Any step produces an error or unexpected result.
- Dropdown empty or missing items.

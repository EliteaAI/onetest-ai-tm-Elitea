---
id: ELITEA-2655
title: "Verify agent acknowledges and adjusts response based on mid-turn input"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled
- User has an active chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "List 10 popular programming languages" |
| Mid-turn message | "Actually, focus only on languages used for data science" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the initial prompt to start agent turn | Agent begins generating list of programming languages |
| 2 | While agent is generating, send the mid-turn interjection | Mid-turn message is sent with "sent while running" indicator |
| 3 | Wait for the agent to complete its response | Agent completes the turn |
| 4 | Review the agent's response content | Response reflects the mid-turn guidance (focuses on data science languages) |

## Expected Final State

Agent's final response incorporates the mid-turn input, demonstrating that the interjection was received and processed.

## Pass/Fail Criteria

**Pass:**
- Agent response reflects the mid-turn guidance
- Response content changes direction based on interjection
- No error messages or failures

**Fail:**
- Agent ignores the mid-turn input
- Response does not incorporate the guidance
- Error occurs during processing

---
id: ELITEA-2870
title: "Verify status transitions from queued to delivered"
priority: high
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, status, ui]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agent/LLM run active and able to accept interjections

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Interjection | "Test status transition" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run | Run begins |
| 2 | Queue interjection during run | Message appears in waiting area with "Queued" status |
| 3 | Observe when agent/LLM picks up the interjection | Message moves to timeline |
| 4 | Verify label in timeline | "Sent while running" label visible |
| 5 | Verify queue count decrements | Count decreases when message picked up |
| 6 | Wait for processing to complete | Response appears for interjection |
| 7 | Reload page | Interjection persists with "Sent while running" label |

## Expected Final State

- Interjection in correct chronological position in timeline
- "Sent while running" label persists after reload
- Response paired with interjection

## Pass/Fail Criteria

**Pass:**
- Initial "Queued" status shown
- Transitions to timeline with "Sent while running" label
- Queue count decrements correctly
- Persists correctly after reload

**Fail:**
- Status transitions missing or incorrect
- "Sent while running" label not shown
- Lost after page reload
- Wrong position in timeline

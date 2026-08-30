---
id: ELITEA-2944
title: "Verify queued messages processed in FIFO order"
priority: critical
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, queue, bug-6457]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6457]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Feature enabled at platform and project level
- Agent/LLM capable of extended processing time

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Message A | Initial task message |
| Message B | "First interjection" |
| Message C | "Second interjection" |
| Message D | "Third interjection (sent after initial response)" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send message A to start agent/LLM processing | Agent/LLM begins processing |
| 2 | While processing, send message B | Message B queued as "Waiting messages · 1" |
| 3 | Send message C | Message C queued as "Waiting messages · 2" |
| 4 | Wait for initial response to start streaming | Initial response begins appearing |
| 5 | Immediately send message D before B and C are processed | Message D queued after B and C |
| 6 | Observe processing order of all messages | Messages processed: A → B → C → D |

## Expected Final State

- All messages processed in strict FIFO order
- Four distinct responses in conversation
- No duplicate responses

## Pass/Fail Criteria

**Pass:**
- Processing order is exactly A → B → C → D
- Message D does NOT jump ahead of B or C
- Each message gets exactly one response
- No duplicates

**Fail:**
- Message D processed before B or C
- Duplicate responses generated
- Messages processed out of order

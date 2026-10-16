---
id: ELITEA-3925
title: "[EliteaAI/elitea_issues#5844] ADO Toolkit: Session Boundary (Cache Persistence)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-3925: ADO Toolkit — Session Boundary (In-Memory Cache Only)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Confirm cache is in-memory only and NOT persistent across agent/runtime restarts.

## Preconditions

- ADO toolkit with `process_images: true`
- Multiple ADO pages/items with same images
- Can control agent/toolkit restart
- LLM/tool logs visible in both sessions

## Test Data

| Session | Action |
|---------|--------|
| Session A | Read/process image once |
| Restart | Agent/toolkit/runtime restart |
| Session B | Read/process same image again |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In session A, read ADO page/item with image using `process_images=true`. | Image described via LLM. |
| 2 | Check logs in session A: verify first LLM vision call. | LLM called; description cached. |
| 3 | Restart the agent/toolkit/runtime. | Session A ends; cache cleared. |
| 4 | In session B (new instance), read same ADO page/item with same image. | Page/item retrieved. |
| 5 | Verify image description present. | Image has description. |
| 6 | Check logs in session B: verify NEW LLM vision call (not cache hit). | **Second LLM call logged** despite same image. |
| 7 | Confirm descriptions are similar but from separate LLM invocations. | Two separate API requests made. |
| 8 | Verify cache is not persisted across restarts. | No disk-based or persistent cache reuse. |

## Expected Final State

- New LLM call after restart
- Cache NOT persisted across sessions
- In-memory only caching confirmed
- No persistent cache mechanism

## Pass/Fail Criteria

**Pass:** New LLM call in session B; cache not persisted; in-memory behavior confirmed.  
**Fail:** Same cache reused; only 1 LLM call total; persistent cache detected.

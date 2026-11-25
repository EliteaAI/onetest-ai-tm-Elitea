---
id: ELITEA-4527
title: "Verify an invalid API key or provider error produces a clear message and the agent run continues"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit configured with a deliberately invalid API key, attached to an agent

## Test Data

| Field | Value |
|-------|-------|
| Invalid key toolkit | Attached to an agent |
| Trigger prompt | A question that would trigger `web_search` |
| No-results query | A nonsense query on a valid-key toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ask the agent (invalid key) a question that triggers `web_search` | A clear error message about the tool call failing (e.g. referencing an authentication/key problem) is shown — no raw stack trace, and the key value is never shown |
| 2 | Continue the conversation after the failed call | Agent responds normally to further messages; the run is not aborted |
| 3 | Using a toolkit with a valid key, query something expected to return no results | A clear "no results" style message is returned, not an error or crash |

## Expected Final State

Both key-invalid and no-results scenarios produce clean, non-crashing, non-key-leaking behavior.

## Pass/Fail Criteria

**Pass:**
- Error messages are clear and clean
- The key is never exposed
- The run/conversation continues afterward

**Fail:**
- A raw exception/stack trace appears
- The key is exposed
- The run/conversation is aborted

---
id: ELITEA-3229
title: "Verify malformed date filter values are handled gracefully"
priority: high
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit and GitLab Org toolkit configured

## Test Data

| Field | Value |
|-------|-------|
| `created_after` (malformed) | `"not-a-date"` |
| `created_after` (impossible range) | Later than `created_before` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `created_after="not-a-date"` on the plain GitLab toolkit | The tool returns a readable error (via `ToolException`) rather than an unhandled exception |
| 2 | Repeat the same malformed value on the GitLab Org toolkit | The tool returns a readable error rather than an unhandled exception |
| 3 | Invoke `get_issues` with `created_after` set later than `created_before` (an impossible range) | An empty result is returned, not an error |

## Expected Final State

Malformed date strings produce a readable tool error rather than a crash, and an impossible date range produces an empty result, on both toolkits.

## Pass/Fail Criteria

**Pass:**
- A non-ISO/invalid date string produces a readable `ToolException` on both toolkits
- An impossible `created_after`/`created_before` range returns an empty result, not an error

**Fail:**
- A malformed date string causes an unhandled exception or crash
- An impossible date range raises an error instead of returning empty

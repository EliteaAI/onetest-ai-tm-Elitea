---
id: ELITEA-3222
title: "Verify labels filter narrows get_issues results"
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
- Test repository has issues tagged with at least 2 distinct labels (e.g. `bug`, `feature`)

## Test Data

| Field | Value |
|-------|-------|
| `labels` (single) | `bug` |
| `labels` (multiple) | `bug,feature` |
| `state` + `labels` combined | `state=closed`, `labels=bug` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `labels=bug` | Only issues tagged `bug` are returned |
| 2 | Invoke `get_issues` with `labels=bug,feature` (comma-separated) | Issues matching either label are returned, per GitLab's label-filter semantics |
| 3 | Combine `labels=bug` with `state=closed` in a single call | Results satisfy both filters simultaneously (AND semantics) |
| 4 | Repeat steps 1–3 against the GitLab Org toolkit | Same filtering behavior is observed |

## Expected Final State

The `labels` filter narrows `get_issues` results correctly for single labels, comma-separated multiple labels, and in combination with `state`, on both toolkits.

## Pass/Fail Criteria

**Pass:**
- Single-label filtering returns only matching issues
- Multi-label filtering returns issues matching any listed label
- Combining `labels` with `state` applies both filters together
- GitLab Org toolkit matches this behavior

**Fail:**
- Unrelated issues appear in a labels-filtered result
- Comma-separated labels are treated as one malformed label
- Combining filters ignores one of them

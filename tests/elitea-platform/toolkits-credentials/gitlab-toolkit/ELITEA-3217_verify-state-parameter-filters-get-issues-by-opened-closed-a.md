---
id: ELITEA-3217
title: "Verify state parameter filters get_issues by opened, closed, and all"
priority: critical
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit and GitLab Org toolkit both configured with valid credentials
- Test GitLab repository has a mix of `opened` and `closed` issues

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| `state` values under test | `opened`, `closed`, `all` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `state=opened` on the plain GitLab toolkit | Only open issues are returned |
| 2 | Invoke `get_issues` with `state=closed` | Only closed issues are returned, including issues that were previously unreachable before the fix |
| 3 | Invoke `get_issues` with `state=all` | Both opened and closed issues are returned together |
| 4 | Repeat steps 1–3 against the GitLab Org toolkit's `get_issues`, with `repository` set | Results match the equivalent plain-toolkit calls for the same repository |

## Expected Final State

`state=opened`, `state=closed`, and `state=all` each return the correctly filtered issue set on both toolkits.

## Pass/Fail Criteria

**Pass:**
- `state=opened` returns only open issues
- `state=closed` returns only closed issues, previously unreachable issues included
- `state=all` returns the union of open and closed issues
- GitLab Org toolkit produces matching results for each state value

**Fail:**
- Any `state` value returns issues outside its expected state
- `state=closed` still fails to surface closed issues
- `state=all` omits either opened or closed issues

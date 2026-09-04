---
id: ELITEA-3220
title: "Verify GitLab Org toolkit get_issues achieves parity with GitLab toolkit"
priority: critical
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab Org toolkit configured with access to at least two different repositories in the org
- Plain GitLab toolkit configured with access to the same repositories, for comparison

## Test Data

| Field | Value |
|-------|-------|
| `state` | `closed` |
| `labels` | `bug` |
| `repository` (call 1) | Test repo A in the org |
| `repository` (call 2) | Test repo B in the org |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` on the GitLab Org toolkit specifying `repository=<repo A>`, `state=closed`, explicit `page`/`per_page`, and `labels=bug` | Call completes successfully |
| 2 | Compare the result against the same call made via the plain GitLab toolkit for repo A | Results match |
| 3 | Switch `repository` to repo B and repeat the same call | Results are scoped correctly to repo B, distinct from repo A's results |

## Expected Final State

The GitLab Org toolkit's `get_issues` behaves identically to the plain GitLab toolkit across state, pagination, and filters, correctly scoped per repository.

## Pass/Fail Criteria

**Pass:**
- GitLab Org toolkit results match the plain GitLab toolkit's results for the same repository and parameters
- Switching `repository` correctly re-scopes results to the new repo

**Fail:**
- GitLab Org toolkit results diverge from the plain GitLab toolkit for equivalent parameters
- Results from repo A leak into or persist when querying repo B

---
id: ELITEA-3225
title: "Verify enriched get_issues output fields are present and accurate"
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
- A known test issue with verifiable `state`, `labels`, `author`, `created_at`, `updated_at` in the GitLab UI
- An issue with no author metadata available (e.g. authored by a deleted/anonymized account), if obtainable

## Test Data

| Field | Value |
|-------|-------|
| Known issue | Issue with verifiable `state`/`labels`/`author`/`created_at`/`updated_at` |
| No-author issue | Issue where `issue.author` is falsy/unavailable |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` on the known test issue | Response returned successfully |
| 2 | Compare each of `state`, `labels`, `author`, `created_at`, `updated_at` in the response against the same issue's data in the GitLab UI | All fields match the real GitLab data |
| 3 | Find or create an issue with no author metadata available and invoke `get_issues` on it | `author` is returned as `None`/null rather than raising an error |
| 4 | Repeat steps 1–3 against the GitLab Org toolkit | Same enriched fields and fallback behavior are observed |

## Expected Final State

Every returned issue object includes accurate `state`, `labels`, `author`, `created_at`, and `updated_at` fields, with `author` gracefully falling back to null when unavailable, on both toolkits.

## Pass/Fail Criteria

**Pass:**
- All enriched fields match the real GitLab data for a known issue
- Missing author metadata results in `author: None`, not an error
- GitLab Org toolkit matches this behavior

**Fail:**
- Any enriched field is missing, stale, or inaccurate
- A missing-author issue raises an error instead of returning `None`

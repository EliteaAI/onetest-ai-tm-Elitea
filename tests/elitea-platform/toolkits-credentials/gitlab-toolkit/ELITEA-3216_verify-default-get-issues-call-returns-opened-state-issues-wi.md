---
id: ELITEA-3216
title: "Verify default get_issues call returns opened-state issues with correct enriched fields"
priority: critical
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit configured with a valid Personal Access Token on a test agent
- Test GitLab repository has both `opened` and `closed` issues, with more than 20 open issues
- Access to Toolkit Test Settings panel

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Repository | Test GitLab repo with 30+ issues (mixed states) |
| `get_issues` params | (all blank/default) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Toolkit Test Settings, invoke `get_issues` on the plain GitLab toolkit with all fields left blank/default | Call completes successfully |
| 2 | Inspect the returned issue list's states | Only issues with state `opened` are returned |
| 3 | Count the returned issues | At most 20 items are returned (default `per_page`), even though the repo has more than 20 open issues |
| 4 | Inspect each returned issue object | Each includes `title`, `number`, `state`, `labels`, `author`, `created_at`, and `updated_at`, all populated with valid, correctly-typed values |
| 5 | Re-run any existing Pipeline or Agent that consumes `get_issues` output | It completes successfully and produces correct downstream results with this response shape |
| 6 | Repeat steps 1–4 against the GitLab Org toolkit's `get_issues`, passing only `repository` | Identical default behavior and output shape are observed |

## Expected Final State

Both the GitLab toolkit and GitLab Org toolkit return a default `get_issues` result limited to open issues, capped at 20 items, with all enriched fields populated.

## Pass/Fail Criteria

**Pass:**
- Only `opened` issues are returned by default
- Result is capped at 20 items when more than 20 open issues exist
- All enriched fields (`title`, `number`, `state`, `labels`, `author`, `created_at`, `updated_at`) are present and valid on every issue
- GitLab Org toolkit matches the same default behavior

**Fail:**
- Closed issues appear in the default result
- More than 20 issues are returned without explicit pagination
- Any enriched field is missing, null where data exists, or malformed
- GitLab Org toolkit default behavior diverges from the plain GitLab toolkit

---
id: ELITEA-1078
title: "GitLab - get_issue Returns Empty Array When Issue Has Zero Comments"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [r-2.0.2]
requirements: [EliteaAI/elitea_issues#4055]
---
# ELITEA-1078: GitLab - get_issue Returns Empty Array When Issue Has Zero Comments

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the edge case where an issue has no comments returns `comments: []` (empty JSON array), not `"[]"` (empty string), `null`, or a missing field.

**Coverage:**
- Empty comments scenario handled correctly post-fix
- `comments` key is present in response
- Value is `[]` (array type), not a string, null, or absent

## Preconditions

- Logged into {{base_url}} (stage environment)
- A GitLab issue exists in the test repo with zero comments
- GitLab toolkit configured with `get_issue` tool enabled

## Test Data

- Issue: no comments (comment count = 0)
- Expected output: {"title": "...", "body": "...", "comments": []}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Toolkit Test Settings for the configured GitLab toolkit | Panel loads |
| 2 | Execute `get_issue` with the issue number that has 0 comments | Tool output displayed |
| 3 | Verify the response contains `comments` key | Key is present |
| 4 | Verify `comments` value is [] (empty JSON array) | Value is [], not "[]" or null |
| 5 | Verify the response contains `title` and `body` fields with correct content | Other fields are unaffected and populated correctly |

## Expected Final State

Other fields are unaffected and populated correctly

## Pass/Fail Criteria

**Pass:**
- Response includes `"comments": []`
- `comments` is array type, not string
- `title` and `body` fields are intact

**Fail:**
- `comments` is "[]" (string)
- `comments` field is missing from the response
- Tool throws an error on a zero-comment issue

---
id: ELITEA-1079
title: "GitLab - get_issue Comment Objects Contain Accessible body and user Fields"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [r-2.0.2]
requirements: [EliteaAI/elitea_issues#4055]
---
# ELITEA-1079: GitLab - get_issue Comment Objects Contain Accessible body and user Fields

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify each element in the returned `comments` array is a dict with `body` (string) and `user` (string) fields matching the actual GitLab comment content.

**Coverage:**
- `body` field contains comment text as plain string
- `user` field contains the commenter's GitLab username as plain string
- Field access does not throw errors
- Values match actual comment content visible in GitLab UI

## Preconditions

- Logged into {{base_url}} (stage environment)
- Test GitLab issue with 2 comments: known body text and known commenter usernames
- GitLab toolkit configured with `get_issue` tool enabled

## Test Data

- Comment 1: body = "Automated test comment from GL15 at 20260226-095218", user = known GitLab bot username
- Comment 2: body = any second distinct comment, user = known GitLab username

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Toolkit Test Settings and execute `get_issue` on the test issue | Output JSON displayed |
| 2 | From the `comments` array, select element at index 0 | First comment object retrieved |
| 3 | Read the `body` key from the element | Returns the first comment's text as a plain string — no repr() escaping |
| 4 | Read the `user` key from the element | Returns the GitLab username as a plain string |
| 5 | Cross-check `body` and `user` values against the actual comments visible in the GitLab issue UI | Values match exactly |
| 6 | Select element at index 1 and repeat the body/user check | Second comment's data is also correctly structured with accurate body and user values |

## Expected Final State

Second comment's data is also correctly structured with accurate body and user values

## Pass/Fail Criteria

**Pass:**
- Each comment element has `body` (non-empty string) and `user` (non-empty string)
- Values match actual comment content in GitLab
- No KeyError, AttributeError, or type error when accessing fields

**Fail:**
- `body` or `user` key is missing from any comment object
- Value is a nested dict, list, or non-string type
- Values do not match actual GitLab comment content

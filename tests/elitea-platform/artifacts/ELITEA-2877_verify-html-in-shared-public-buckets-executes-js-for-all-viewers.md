---
id: ELITEA-2877
title: "Verify HTML files in shared/public buckets execute JS for all viewers"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176]
---

## Preconditions

- Two ELITEA user accounts are available
- A bucket shared with a second user (or made public) exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | Any JS-containing HTML file, uploaded to a shared/public bucket |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload a JS-containing HTML file to a bucket shared with another user (or made public) | Upload succeeds |
| 2 | As a second user (or different account), open the file in Preview mode | File opens for the second user |
| 3 | Observe JS execution for the second user | JS executes correctly |
| 4 | Confirm sandbox isolation for the second user | Second user's session data is also not accessible from the iframe |

## Expected Final State

JS execution behavior and sandbox isolation are consistent regardless of bucket visibility (private/shared/public) or viewing user.

## Pass/Fail Criteria

**Pass:**
- JS executes identically for the second user, with sandbox isolation intact

**Fail:**
- JS fails to execute for the second user, or sandbox isolation is weaker for shared/public buckets

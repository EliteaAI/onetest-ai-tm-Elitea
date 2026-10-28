---
id: ELITEA-4205
title: "Skill instructions save at exactly 50000 characters; UI blocks further input and API rejects over-limit content"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:agents, feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6744]
---

## Preconditions

- User is logged in to `{{base_url}}` with Skill creation permissions.
- Platform is at the default "Skill Content Max Length" of 50000 characters.

## Test Data

| Field | Value |
|-------|-------|
| Exact-limit instructions | A string of exactly 50000 characters |
| Over-limit instructions | A string of 50001 characters |
| Under-limit instructions | A string of 10000 characters |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Skill editor (new or existing Skill) and type or paste instructions past 50000 characters | Input is hard-blocked at exactly 50000 characters; no further characters can be typed or pasted |
| 2 | Observe the character counter while at the cap | Counter shows "0 characters left"; no error message is shown (expected behavior, not a defect) |
| 3 | Paste a block of text that would take the editor from under the limit to over 50000 characters in one paste | Pasted text is truncated to land exactly at 50000 characters; no error shown, no crash |
| 4 | Save a Skill with instructions at exactly 50000 characters via the UI | Save succeeds |
| 5 | Call the Skill create/update API directly with instructions at 50001 characters (bypassing the UI's input block) | Request is rejected with an error naming the 50000-character limit |
| 6 | Call the same API with instructions at exactly 50000 characters | Request succeeds |
| 7 | Save a Skill with instructions well under the limit (e.g., 10000 characters) via the UI | Save succeeds; the counter decrements correctly as characters are typed |

## Expected Final State

The 50000-character limit is enforced identically by the UI (hard input block, no error) and the API (save-time rejection with a limit-naming error); content at or under 50000 characters always saves successfully.

## Pass/Fail Criteria

**Pass:**
- All steps behave as described.
- No way exists to save instructions over 50000 characters through either the UI or the API.

**Fail:**
- The UI allows typing or pasting past 50000 characters.
- The API accepts instructions over 50000 characters.
- A Skill at exactly 50000 characters fails to save via either path.

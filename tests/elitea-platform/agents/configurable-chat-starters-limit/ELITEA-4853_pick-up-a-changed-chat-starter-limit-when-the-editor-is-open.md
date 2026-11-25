---
id: ELITEA-4853
title: "Pick up a changed chat starter limit when the editor is opened without a page reload"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin in two browser contexts (A and B)
- The platform limit M is 6 (restore the original value at the end)
- An agent with 4 starters and a pipeline with 8 starters exist

## Test Data

| Field | Value |
|-------|-------|
| Limit change | 6 → 7 |
| Expected agent counter | "4/6" → "4/7" |
| Expected pipeline counter | "8/7" (over limit) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Context A: open the 4-starter agent editor | The counter reads "4/6 starters added." |
| 2 | Context A: go to the Agents list using in-app navigation | The list is shown |
| 3 | Context B: in Admin → Features → Chat Starters set 7 and Save | Saved |
| 4 | Context A: open the same agent again through in-app navigation only (no reload) | The counter reads "4/7"; DevTools → Network shows a new `platform_settings` request |
| 5 | Context A: open the 8-starter pipeline the same way | The counter reads "8/7" in the over-limit state |
| 6 | Restore the original limit | Restored |

## Expected Final State

Opening an editor always uses the current platform limit, with no reload needed.

## Pass/Fail Criteria

**Pass:**
- The counter reflects the new M on the next editor open without a page reload

**Fail:**
- The editor shows the old M until the page is reloaded

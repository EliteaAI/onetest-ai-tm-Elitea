---
id: ELITEA-4543
title: "Verify empty/default Allowed Domains and Blocked Domains fields do not restrict tool behavior"
priority: medium
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with Allowed Domains and Blocked Domains both left empty (default)

## Test Data

| Field | Value |
|-------|-------|
| Allowed Domains | Empty |
| Blocked Domains | Empty |
| Target domain | Any arbitrary public domain |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or edit a Tavily toolkit leaving both fields empty | Fields display as empty, not a placeholder that could be mistaken for a real restriction |
| 2 | Run `web_search` and `web_extract` against an arbitrary public domain | Neither is blocked or restricted in any way |
| 3 | Check both fields in create and edit views | Both consistently display as empty in each view |

## Expected Final State

Empty domain fields are confirmed to impose no unintended restriction.

## Pass/Fail Criteria

**Pass:**
- No domain restriction occurs when both fields are empty
- The fields display as genuinely empty in both views

**Fail:**
- Any domain is unexpectedly blocked/restricted
- An empty field displays a misleading placeholder value

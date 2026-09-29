---
id: ELITEA-3462
title: "Icon Color Updates Immediately After Restrict Access"
priority: high
type: regression
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, ui, bug-verification, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283, EliteaAI/elitea_issues#6776]
---
# ELITEA-3462: Icon Color Updates Immediately After Restrict Access

**Module:** Conversations · **Priority:** High · **Type:** Regression / Bug Verification

**Objective:** Verify that the sharing icon color updates immediately after restricting access (Bug #6776 verification).

**Bug Reference:** [#6776](https://github.com/EliteaAI/elitea_issues/issues/6776) - Conversation icon color does not update immediately after "Restrict access"

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists (sharing icon is GREEN)

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Initial State | Public (green icon) |
| Bug | #6776 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Identify public conversation in sidebar | Green sharing icon visible |
| 2 | Right-click and select "Restrict access" | Wizard opens |
| 3 | Select only the author | Only author chip selected |
| 4 | Click "Restrict access" button | Wizard closes |
| 5 | IMMEDIATELY check sharing icon in sidebar | Icon should turn GREY immediately |
| 6 | Do NOT refresh the page | Observe icon color |
| 7 | Wait 5 seconds | Icon should remain grey |
| 8 | Refresh page | Icon is still grey (persisted) |

## Expected Final State

- Icon turns grey immediately without page refresh
- Behavior matches "Make public" (which turns green immediately)

## Pass/Fail Criteria

**Pass:**
- Step 5: Icon turns grey immediately after wizard closes (no refresh needed)

**Fail (Bug #6776):**
- Step 5: Icon stays green until page refresh

## Teardown

- None required

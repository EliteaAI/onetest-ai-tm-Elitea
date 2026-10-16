---
id: ELITEA-3845
title: "Validation report - copy and full-screen include all findings"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with publish permissions
- Test agent with multiple validation findings (agent + Skills)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Description | Too short |
| Skill A | Contains placeholder |
| Skill B | Contains secrets |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set up agent with multiple findings | Multiple issues present |
| 2 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 3 | Wait for validation | Result: **FAIL** |
| 4 | Click **Copy** button | Report copied to clipboard |
| 5 | Paste and review | Report includes ALL findings: description + Skills |
| 6 | Verify each finding has proper attribution | Each finding shows its source context |
| 7 | Click **Full-screen** button | Validation Details dialog |
| 8 | Verify all findings visible | All findings displayed |
| 9 | Expand each finding | Details and fix suggestions visible |
| 10 | Verify consistent format | Skill findings formatted same as agent findings |
| 11 | Close full-screen | Return to wizard |

## Expected Final State

Validation report (copy and full-screen view) includes all findings with proper attribution for both agent and Skill issues. Consistent formatting across all finding types.

## Pass/Fail Criteria

**Pass:**
- Copy report includes all findings with attribution
- Full-screen view shows all findings with expand/collapse
- Consistent formatting between agent and Skill findings

**Fail:**
- Some findings missing from copy or full-screen
- Inconsistent formatting
- Attribution missing or incorrect

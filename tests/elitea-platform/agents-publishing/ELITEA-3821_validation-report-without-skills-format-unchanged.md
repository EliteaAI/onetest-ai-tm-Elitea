---
id: ELITEA-3821
title: "Validation report without skills - format unchanged"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with `models.applications.publish.post` permission
- Test agent created with intentional WARNING (e.g., short description)
- Agent has NO Skills attached (0/5)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "No Skills Warning Agent" |
| Skills Attached | 0 (none) |
| Issue | Short description (triggers WARNING) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create agent with intentional WARNING (e.g., short description) | Agent with non-Skill warning |
| 2 | Ensure NO Skills attached | 0/5 Skills |
| 3 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 4 | Review validation findings | Warnings shown for description (not Skills) |
| 5 | Verify NO Skill-related findings | No findings with `skill:` context |
| 6 | Click **Copy** button | Validation report copied |
| 7 | Paste and review report | Report format unchanged; no Skills section |
| 8 | Click **Full-screen** | Validation Details dialog |
| 9 | Verify no Skills section in full details | Standard validation output only |
| 10 | Acknowledge warnings and Publish | Publishes successfully |

## Expected Final State

Validation report format remains unchanged for agents without Skills. No Skills section appears in copy or full-screen view.

## Pass/Fail Criteria

**Pass:**
- Validation report format unchanged
- No Skills section appears in copy or full-screen view
- No `skill:` context in any findings
- Standard warnings display correctly

**Fail:**
- Report format changed for agents without Skills
- Skills section appears when no Skills attached
- Standard validation behavior affected

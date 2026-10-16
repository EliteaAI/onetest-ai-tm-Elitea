---
id: ELITEA-3843
title: "Incremental fix - validation updates correctly"
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
- User has editor/admin role with publish permissions
- Test agent with multiple CRITICAL findings: agent description + 2 Skills with issues
- All issues identified from prior validation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Description | Too short (below minimum) |
| Skill A | Contains placeholder "TODO" |
| Skill B | Contains hardcoded API key |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Verify agent has 3 CRITICAL findings | Description, Skill A, Skill B |
| 2 | Fix agent description (make longer) | Save change |
| 3 | Re-validate | Validation runs |
| 4 | Verify description CRITICAL resolved | No finding for description |
| 5 | Verify Skill A and Skill B criticals remain | Still 2 CRITICAL findings |
| 6 | Verify **Publish** button still disabled | Cannot publish |
| 7 | Fix Skill A (remove placeholder) | Save change |
| 8 | Re-validate | Validation runs |
| 9 | Verify Skill A CRITICAL resolved | Only Skill B finding remains |
| 10 | Verify **Publish** button still disabled | 1 CRITICAL remains |
| 11 | Fix Skill B (remove API key) | Save change |
| 12 | Re-validate | Result: **PASS** |
| 13 | Verify **Publish** button enabled | All criticals resolved |

## Expected Final State

Fixing validation issues one at a time correctly updates the validation results. Publish is only enabled when all criticals are resolved.

## Pass/Fail Criteria

**Pass:**
- Fixing issues removes their findings from results
- Publish blocked while ANY critical exists
- After all fixes, Publish enabled

**Fail:**
- Fixed issues still show findings
- Publish enabled before all criticals resolved

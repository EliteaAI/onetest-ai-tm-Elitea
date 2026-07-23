---
id: ELITEA-2240
title: "Multiple validation issues - correct attribution"
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
- Test agent with multiple Skills, some with issues
- Agent base configuration also has issues (for combination testing)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Description | Too short (below minimum) |
| Skill A | Contains placeholder "TODO" |
| Skill B | Contains hardcoded API key |
| Skill C | Valid content (no issues) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure agent with short description | Agent saved |
| 2 | Attach Skill A (placeholder), Skill B (secrets), Skill C (valid) | 3 Skills attached |
| 3 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 4 | Wait for validation | Result: **FAIL** (multiple criticals) |
| 5 | Count CRITICAL findings | At least 3: description, Skill A, Skill B |
| 6 | Verify description finding context | Context: `description` or `agent description` |
| 7 | Verify Skill A finding context | Context: `skill: Skill A` |
| 8 | Verify Skill B finding context | Context: `skill: Skill B` |
| 9 | Verify Skill C NOT in findings | No findings for valid Skill C |
| 10 | Verify **Publish** button disabled | Cannot publish with any CRITICAL |

## Expected Final State

Multiple validation findings from different sources are all displayed with correct attribution. Each finding shows whether it's from agent component or specific Skill. No findings appear for valid components.

## Pass/Fail Criteria

**Pass:**
- Multiple findings from different sources all displayed
- Each finding correctly attributed (agent component vs. specific Skill)
- No findings for valid components/Skills
- Publish blocked while ANY critical exists

**Fail:**
- Some findings missing
- Incorrect attribution
- Valid components show findings
- Publish enabled despite criticals

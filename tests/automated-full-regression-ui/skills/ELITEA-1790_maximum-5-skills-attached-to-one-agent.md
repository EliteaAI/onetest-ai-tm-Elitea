---
id: ELITEA-1790
title: "Maximum 5 Skills can be attached to one Agent"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1790: Maximum 5 Skills can be attached to one Agent

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that the platform enforces a maximum limit of 5 Skills per Agent, and that attempting to attach a 6th Skill is blocked with an appropriate error or UI indication.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- At least 6 distinct Skills exist in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Number of Skills to create | 6 (Skill 1 through Skill 6) |
| Maximum allowed Skills per Agent | 5 |
| Agent name | (any new Agent name, e.g. "Multi-Skill Agent") |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or confirm 6 distinct Skills exist in the project | 6 Skills are available to attach |
| 2 | Navigate to Agents and create a new Agent or open one in edit mode | Agent creation / edit form is open |
| 3 | Attach Skill 1 to the Agent | Skill 1 is listed as attached |
| 4 | Attach Skill 2 to the Agent | Skill 2 is listed as attached |
| 5 | Attach Skill 3 to the Agent | Skill 3 is listed as attached |
| 6 | Attach Skill 4 to the Agent | Skill 4 is listed as attached |
| 7 | Attach Skill 5 to the Agent | Skill 5 is listed as attached; 5 Skills are now attached |
| 8 | Attempt to attach Skill 6 to the Agent | The action is blocked; an error message or disabled state indicates the limit of 5 has been reached |
| 9 | Save the Agent with 5 Skills attached | Agent saves successfully with exactly 5 Skills attached |

---

## Expected Final State

The Agent is saved with exactly 5 Skills. The 6th attachment attempt is rejected by the UI, and no more than 5 Skills can be attached to a single Agent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors up to step 7.
- Step 8 is blocked with a clear error or UI indication.
- Agent saves with exactly 5 Skills.

**Fail:**
- Any step up to step 7 produces an error.
- The 6th Skill can be attached (limit not enforced).
- Agent fails to save with 5 Skills.

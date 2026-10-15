---
id: ELITEA-1790
title: "Maximum Skills attachable to one Agent is enforced (limit is read live from the platform, not fixed at 5)"
priority: high
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_agent_max_five_skills_limit.TestAgentMaxFiveSkillsLimit.test_max_five_skills_attach_limit
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2449
---

# ELITEA-1790: Maximum Skills attachable to one Agent is enforced (limit is read live from the platform, not fixed at 5)

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that the platform enforces a maximum limit of Skills per
Agent, and that attempting to attach one more Skill than the limit allows is
blocked with an appropriate error or UI indication.

> **Case-text update, 2026-10-15 (tracking issue #2443, EL-6930):** this case
> previously hardcoded the limit at 5. As of EliteaUI commit `8a1ae6b9`
> (2026-10-13), the platform reads the limit from the `application_skills`
> API's `max_skills` field (currently **50** on DEV) rather than a frontend
> constant. The limit is **not** configurable per-project or per-agent — there
> is no admin/project-settings control and no API field to change it; it is a
> global server-side value. This case now describes the *mechanism*
> (enforcement at whatever the live limit is) rather than a literal number, so
> it stays correct if the platform's limit changes again. See the automation
> AFS's `## Adjustment — 2026-10-15` section
> (`test-specs/skills/lp1_max-5-skills-per-agent_ELITEA-1790.md`) for the full
> investigation and the chosen automation design (bulk setup via API for the
> skills below the boundary, with the boundary-crossing attach and the
> over-limit attempt still exercised through the real UI).

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- At least `N + 1` distinct Skills exist in the project, where `N` is the
  platform's current maximum Skills-per-Agent limit (read from the
  `application_skills` API's `max_skills` field — do not assume a fixed
  number).

---

## Test Data

| Field | Value |
|-------|-------|
| Number of Skills to create | `N + 1` (N to reach the limit, plus 1 to confirm the over-limit attempt is blocked) |
| Maximum allowed Skills per Agent | **Read live from the platform** (`application_skills.max_skills`) — currently 50 on DEV as of 2026-10-15; was 5 before EL-6930 (2026-10-13). Do not hardcode either number in automation. |
| Agent name | (any new Agent name, e.g. "Multi-Skill Agent") |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or confirm `N + 1` distinct Skills exist in the project | `N + 1` Skills are available to attach |
| 2 | Navigate to Agents and create a new Agent or open one in edit mode | Agent creation / edit form is open |
| 3 | Attach Skills 1 through `N - 1` to the Agent, one at a time | Each Skill is listed as attached; the counter increments toward `N` |
| 4 | Attach the `N`th Skill to the Agent (the boundary attach) | The `N`th Skill is listed as attached; the counter reads `N/N` and the add-skill control becomes disabled, with a tooltip explaining why |
| 5 | Attempt to attach the `(N+1)`th Skill to the Agent | The action is blocked; an error message or disabled state indicates the limit of `N` has been reached |
| 6 | Save the Agent with exactly `N` Skills attached | Agent saves successfully with exactly `N` Skills attached |

---

## Expected Final State

The Agent is saved with exactly `N` Skills, where `N` is the platform's
current live limit. The `(N+1)`th attachment attempt is rejected by the UI,
and no more than `N` Skills can be attached to a single Agent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors through attaching the `N`th Skill.
- The attempt to attach the `(N+1)`th Skill is blocked with a clear error or
  UI indication.
- Agent saves with exactly `N` Skills, matching the live `max_skills` value.

**Fail:**
- Any step up to and including the `N`th attach produces an error.
- An `(N+1)`th Skill can be attached (limit not enforced).
- Agent fails to save with exactly `N` Skills.
- The test (or any future automation of this case) hardcodes a literal
  number instead of reading `max_skills` live — this would silently stop
  verifying the real mechanism the next time the platform's limit changes.

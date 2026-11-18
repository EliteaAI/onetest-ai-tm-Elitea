---
id: ELITEA-4733
title: "[Conditional] Invalid agent frontmatter blocks Save and keeps the user's edits (if implemented)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4733: [Conditional] Invalid agent frontmatter blocks Save and keeps the user's edits (if implemented)

**Module:** agents · **Priority:** high · **Type:** functional

> **CONDITIONAL:** Run this case only if agent YAML frontmatter (issue section 4) is implemented. The issue has no linked PRs yet. If frontmatter is not implemented, mark the case SKIPPED with the note "Not implemented — follow-up issue #___".

**Objective:** Verify that invalid agent frontmatter blocks Save and Save As Version with an actionable error, and that the user's draft is never lost.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent YAML frontmatter is implemented on the environment under test.
- Agent "QA-7377 EdgeCases" is open in Edit mode, with no pending changes.

---

## Test Data

| Case | Frontmatter content |
|---|---|
| Broken YAML | `name: [unclosed` |
| Missing closing delimiter | `---` + `name: x` with no closing `---` |
| Empty name | `name: ""` |
| Name over limit | `name:` with a 33-character value (the agent name limit is 32) |
| Empty description | `description:` with no value |
| Unknown key | `foo: bar` |
| Frontmatter removed entirely | The whole `---` block is deleted |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Apply the first case from the Test Data table to the frontmatter. Also add the body line `BODY-7377` | The editor shows the edited content |
| 2 | Click Save | An actionable error explains the problem. Save is blocked. The edited frontmatter and `BODY-7377` are still in the editor |
| 3 | Click Save As Version | The same validation applies. No version is created |
| 4 | Fix the frontmatter so that it is valid, then click Save | Save succeeds without re-entering `BODY-7377` |
| 5 | Repeat steps 1–4 for every other case in the Test Data table | Each case is either rejected with a clear error and no data loss, or accepted as documented (for example, an unknown key is ignored, or a removed block is regenerated from the fields). Write down the actual behavior for each case |
| 6 | Compare the error messages with the skill import error for missing frontmatter | The wording and style of the messages are consistent |

---

## Expected Final State

"QA-7377 EdgeCases" has valid frontmatter and contains `BODY-7377`. No invalid version was created.

---

## Pass/Fail Criteria

**Pass:**
- Invalid frontmatter never saves silently and never removes the user's body content.
- The errors explain how to fix the problem.

**Fail:**
- Invalid data is saved, the draft is lost, the error is generic or missing, or Save As Version skips validation.

---

## Notes

- Related: ELITEA-1900 (agent name limit of 32 characters), ELITEA-2438 (skill import with missing frontmatter), ELITEA-4281 / ELITEA-4287 (skill frontmatter delimiter and deleted-block behavior).

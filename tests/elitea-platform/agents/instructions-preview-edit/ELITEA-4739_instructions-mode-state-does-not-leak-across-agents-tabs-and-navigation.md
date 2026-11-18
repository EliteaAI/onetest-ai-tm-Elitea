---
id: ELITEA-4739
title: "Instructions mode state does not leak across agents, browser tabs, and navigation"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4739: Instructions mode state does not leak across agents, browser tabs, and navigation

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Preview / Edit mode state does not carry over between entities or browser tabs, and that it resets as specified: new unsaved agent → Edit, saved agent → Preview.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agents "QA-7377 Agent" and "QA-7377 Published" (versions `base` and `v1-qa7377`) and skill "qa-7377-skill" exist.

---

## Test Data

| Field | Value |
|-------|-------|
| Agents | QA-7377 Agent; QA-7377 Published |
| Skill (reference behavior) | qa-7377-skill |
| Tab 2 edit text | `TAB-7377` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Put "QA-7377 Agent" in Edit (with no changes), then open "QA-7377 Published" | "QA-7377 Published" opens in Preview |
| 2 | Go back to "QA-7377 Agent" in Preview and click + Agent | The new, unsaved agent opens in Edit |
| 3 | Without saving, go back to "QA-7377 Agent" (discard the draft if asked) | "QA-7377 Agent" opens in Preview |
| 4 | Open "QA-7377 Agent" in two browser tabs. Use Edit in tab 1 and Preview in tab 2 | Each tab keeps its own mode |
| 5 | In tab 1, add `TAB-7377` and click Save. Then refresh tab 2 | Tab 2 shows the saved content, including `TAB-7377`, in Preview |
| 6 | On "QA-7377 Published", switch to Edit (with no changes) and change the version from `base` to `v1-qa7377` | Write down the active mode after the switch. Repeat on "qa-7377-skill" with two versions: the agent and the skill behave the same way |
| 7 | Use browser Back and Forward between the Agents list and the agent details page several times | The Instructions editor renders correctly every time, in the expected default mode |

---

## Expected Final State

"QA-7377 Agent" contains `TAB-7377` (remove it after the run). No unsaved draft agent is left behind.

---

## Pass/Fail Criteria

**Pass:**
- The mode never carries over between entities or tabs.
- Default modes follow the rule (new unsaved → Edit, saved → Preview).
- The behavior after a version switch is the same for agents and skills.

**Fail:**
- One entity's mode carries over to another, a tab shows stale content after refresh, or Back/Forward leaves the editor broken or blank.

---

## Notes

- Default mode rule: QA owner clarification, 2026-11-17.

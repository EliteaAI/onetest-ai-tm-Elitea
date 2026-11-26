---
id: ELITEA-4919
title: "Skill whose instructions point to its reference files answers according to those files"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4919: Skill whose instructions point to its reference files answers according to those files

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that when a skill whose instructions point to its other files is used in a chat, the answer follows what those files say.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `qa-7185-pkg` is imported from P-folder of ELITEA-4916.
- Agent `qa-7185-agent` has `qa-7185-pkg` attached (agent → SKILLS → **Skill** → pick the skill; the counter shows "1/50 skills added.").

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | `qa-7185-agent` |
| Skill | `qa-7185-pkg` |
| Rule in `references/format.md` | Start every answer with `REF-OK:` and end with `-- qa7185` |
| Prompt | "Use the qa-7185-pkg skill and answer: what is a QA report?" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent, click **Test Agent** and send the prompt | Chips "Skill: qa-7185-pkg · Nms" appear. The answer starts with `REF-OK:` and ends with `-- qa7185` |
| 2 | Click a "Skill: qa-7185-pkg" chip | The OUTPUT panel shows the skill instructions and the `<skill_files>` list (`references/ (1 file)`, `scripts/ (1 file)`) |
| 3 | In a new chat with the agent type `~`, pick the skill from MENTION SKILL, then send the same question | The answer has the same format as in step 1 |

---

## Expected Final State

The chats show answers formatted by the rule from `references/format.md`. Delete the chats after the run.

---

## Pass/Fail Criteria

**Pass:**
- The answer follows the rule from `references/format.md`.

**Fail:**
- The answer ignores the reference file, or the skill cannot read it.

---

## Notes

- LLM wording varies; check only the `REF-OK:` prefix and the `-- qa7185` suffix.
- Related: ELITEA-4239, ELITEA-4240.

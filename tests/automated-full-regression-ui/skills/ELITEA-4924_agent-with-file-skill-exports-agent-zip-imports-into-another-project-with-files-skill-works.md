---
id: ELITEA-4924
title: "Agent with a file skill exports as .agent.zip and imports into another project with the skill files, and the skill still works"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:agents, feat:export, feat:import-forking, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4924: Agent with a file skill exports as .agent.zip and imports into another project with the skill files, and the skill still works

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify that an agent whose skill has files exports as `.agent.zip`, and that importing it into another project brings back the agent and the skill with its files, and the skill still works.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in Project A and Project B.
- In Project A, agent `regression-pkg-agent` has skill `regression-skill-pkg` attached, imported from the package ZIP of ELITEA-4922 (**Files – 2**).

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | `regression-pkg-agent` |
| Skill | `regression-skill-pkg`; `references/format.md` says "Start every answer with `REF-OK:` and end with `-- qa7185`" |
| Target project | Project B |
| Prompt | "Use the regression-skill-pkg skill: count the words in "alpha beta gamma delta" and answer in its required format." |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent, then ⋮ → **Export** | `regression-pkg-agent.agent.zip` downloads, containing `regression-pkg-agent.agent.md`, `skills/regression-skill-pkg/references/format.md` and `skills/regression-skill-pkg/scripts/count.py` |
| 2 | Open Agents → **Add** → **Import from file**, choose the ZIP and select Project B in **Import parameters** | The dialog shows the agent and SKILLS "1 of 1 skills selected" |
| 3 | Click **Import** | **Import Complete** lists "1 Agents: regression-pkg-agent" and "1 Skills: regression-skill-pkg" |
| 4 | Click **Got it**, then open the recreated skill in Project B | The agent shows "1/50 skills added.". The skill shows **Files – 2** and "References 1 · Scripts 1" |
| 5 | In Project B open the agent, click **Test Agent** and send the prompt | The answer starts with `REF-OK:`, contains `WORDS= 4` and ends with `-- qa7185` |

---

## Expected Final State

The agent and the skill exist in Project B with the same files. Delete them in both projects after the run.

---

## Pass/Fail Criteria

**Pass:**
- The export is `.agent.zip` with the skill files.
- The import recreates the agent and the skill with **Files – 2**.
- The skill answers in the required format.

**Fail:**
- The export is `.md`, or a skill file is missing in the export or after import.
- The imported skill ignores its files.

---

## Notes

**Source functional tests:** ELITEA-4921 (steps 1–4), ELITEA-4919 (step 1 as the closing check) — AC6 of EliteaAI/elitea_issues#7185
**Regression rationale:** The new agent package format crosses projects and recreates entities.
**Selected checkpoints:** export file name and contents; import preview; Import Complete; file count after import; working skill.
**Not covered:** agents without file skills (covered by ELITEA-1794, ELITEA-1795).

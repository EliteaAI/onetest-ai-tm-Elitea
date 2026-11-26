---
id: ELITEA-4921
title: "Agent whose skill has files exports as .agent.zip and imports into another project with the skill files; agents without such skills are unchanged"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:agents, feat:export, feat:import-forking, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4921: Agent whose skill has files exports as .agent.zip and imports into another project with the skill files; agents without such skills are unchanged

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that an agent whose skill has files exports as `.agent.zip`, that importing it into another project brings back the agent and the skill with its files, and that agents and skills without files export and import as before.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in Project A and Project B.
- Agent G in Project A has `qa-7185-pkg` attached (**Files – 2**, see ELITEA-4916).
- Agent H in Project A has only skills with **Files – 0**.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent with file skill | G |
| Agent without file skills | H |
| Skill | `qa-7185-pkg` |
| Target project | Project B |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open G, then ⋮ → **Export** | `<G>.agent.zip` downloads. It contains `<G>.agent.md` (with the skill instructions embedded) and `skills/qa-7185-pkg/references/format.md`, `skills/qa-7185-pkg/scripts/count.py` |
| 2 | Open Agents → **Add** → **Import from file**, choose the ZIP, select Project B in **Import parameters**, click **Import** | The dialog shows SKILLS "1 of 1 skills selected". **Import Complete** lists "1 Agents" and "1 Skills" |
| 3 | Click **Got it** and open the recreated skill in Project B | The agent shows "1/50 skills added.". The skill shows **Files – 2** with the same Files card counts |
| 4 | In Project B ask G something that triggers the skill (as in ELITEA-4919) | The answer follows `references/format.md` |
| 5 | Export H and import it into Project B | Same `.md` format and import result as before (ELITEA-1794 / ELITEA-1795) |

---

## Expected Final State

Agent G and `qa-7185-pkg` exist in Project B with the same files. Delete the test entities in both projects after the run.

---

## Pass/Fail Criteria

**Pass:**
- The skill files survive the agent export and import.
- Agents without file skills export and import as before.

**Fail:**
- The export is `.md` for G, or a skill file is missing in the export or after import.
- Agent H exports or imports differently than before.

---

## Notes

- Related: ELITEA-4766, ELITEA-1794, ELITEA-1795, ELITEA-1895, ELITEA-1902.

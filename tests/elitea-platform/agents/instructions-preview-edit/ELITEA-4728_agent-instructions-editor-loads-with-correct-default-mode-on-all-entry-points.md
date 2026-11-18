---
id: ELITEA-4728
title: "Agent Instructions editor loads with the correct default mode on all entry points"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4728: Agent Instructions editor loads with the correct default mode on all entry points

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Verify that the new Preview / Edit Instructions editor loads without errors on every surface where agent Instructions can be edited, and that each surface uses the correct default mode (saved agent → Preview; new, unsaved agent → Edit).

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" exists and is saved.
- An agent `.md` export file is available for import (for example, an export of "QA-7377 Agent").
- A second project is available as the fork destination.
- Browser DevTools console is open.

---

## Test Data

| Entry point | Default mode |
|---|---|
| Agents → existing agent details page ("QA-7377 Agent") | Preview |
| Agents → + Agent (new, unsaved agent) | Edit |
| Chat → agent canvas / agent editor opened from a conversation for a new, unsaved agent (Build with AI in chat agent editor flow) | Edit |
| Chat → agent canvas / agent editor opened for an existing, saved agent | Preview |
| Build with AI → review step → created (saved) agent page | Preview |
| Imported agent (from the `.md` file) | Preview |
| Forked agent in the destination project | Preview |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the first entry point from the Test Data table and scroll to INSTRUCTIONS | The section loads fully, with no blank areas. The active mode matches the "Default mode" column |
| 2 | Switch to the other mode, then switch back | Both modes show the same content. The switch responds every time |
| 3 | Check the browser console | No errors related to the Instructions editor |
| 4 | Repeat steps 1–3 for every other row in the Test Data table | Every entry point passes steps 1–3 |
| 5 | Click + Agent. In Edit, enter Name `QA-7377 EntryPoint`, a Description, and Instructions `Entry point check`. Click Save | The agent is created and appears in the Agents list. Its Instructions read "Entry point check" |

---

## Expected Final State

Every entry point shows a working Instructions editor with the correct default mode. Agent "QA-7377 EntryPoint" exists.

---

## Pass/Fail Criteria

**Pass:**
- All seven entry points load the editor without errors and use the expected default mode.
- An agent created through Edit mode saves correctly.

**Fail:**
- Any entry point shows the old editor, a blank or broken section, the wrong default mode, or console errors.

---

## Notes

- Related existing cases to re-run (not duplicated): ELITEA-1871 (Instructions alone do not enable Save on create), ELITEA-1920 (Build with AI in chat agent editor), ELITEA-1901 (import agent .md), ELITEA-1893 (fork agent version).
- Default mode rule: QA owner clarification, 2026-11-17.
- Clean-up: delete "QA-7377 EntryPoint", the imported agent, and the forked copy.

---
id: ELITEA-4732
title: "Agent YAML frontmatter synchronizes with Name and Description"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4732: Agent YAML frontmatter synchronizes with Name and Description

**Module:** agents · **Priority:** high · **Type:** functional

> **CONDITIONAL:** Run this case only if agent YAML frontmatter (issue section 4) is implemented. The issue has no linked PRs yet. If frontmatter is not implemented, mark the case SKIPPED with the note "Not implemented — follow-up issue #___".

**Objective:** Verify two-way synchronization between the agent frontmatter in Edit mode and the GENERAL Name / Description fields, and verify that frontmatter is hidden in Preview.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent YAML frontmatter is implemented on the environment under test.
- Agent "QA-7377 Published" has two versions: `base` and `v1-qa7377`, with different Name or Description values.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | QA-7377 Published |
| New name | `QA-7377 Renamed` |
| New description (set in frontmatter) | `Updated from frontmatter` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Published" (version `base`) and switch to Edit | The source starts with `---`, `name: <current name>`, `description: <current description>`, `---` |
| 2 | Change the GENERAL Name field to `QA-7377 Renamed` | The frontmatter `name:` updates right away |
| 3 | In the frontmatter, change `description:` to `Updated from frontmatter` | The GENERAL Description field updates |
| 4 | Switch to Preview | The frontmatter block is not shown. Only the body is rendered |
| 5 | Click Save and reload the page | Name, Description and frontmatter all show the saved values. The Agents list card and the chat participant name show `QA-7377 Renamed` |
| 6 | Select version `v1-qa7377` | The frontmatter shows that version's Name / Description |
| 7 | Export the agent as `.md`, then import the file | The imported agent has a single frontmatter block (no duplicate) with the correct name and description |

---

## Expected Final State

"QA-7377 Published" base version is named `QA-7377 Renamed`, with the description `Updated from frontmatter`. Restore the original values after the run.

---

## Pass/Fail Criteria

**Pass:**
- Frontmatter and the GENERAL fields stay in sync in both directions, and across versions and export/import.
- Preview never shows frontmatter.

**Fail:**
- The fields and the frontmatter diverge, frontmatter shows in Preview, or export/import duplicates the frontmatter.

---

## Notes

- Related existing skill cases (model behavior): ELITEA-4277, ELITEA-4278, ELITEA-4282. Related agent cases: ELITEA-1894 (export), ELITEA-1901 (import).
- If the agent is published to Agent Hub / Catalog, also check the catalog card name.

---
id: ELITEA-4766
title: "Skill frontmatter survives skill publish, agent publish, agent Markdown export/import and fork"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:publishing, feat:fork, feat:agents]
requirements: [EliteaAI/elitea_issues#7183]
---

# ELITEA-4766: Skill frontmatter survives skill publish, agent publish, agent Markdown export/import and fork

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that a skill's licence, extra frontmatter keys, tags and run settings are kept when the skill is published, when an agent with the skill is published, exported as Markdown and imported, and when the skill or agent is forked.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in Project A and Project B.
- Skill S1 is imported from file B of ELITEA-4761, with tags and custom run settings added and instructions of at least 100 characters.
- Skill S2 has `license: MIT`, tags and custom run settings.
- Agent G in Project A has S1 and S2 attached. S1 and S2 have no files (**Files – 0**), so agent G exports as Markdown.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skills | S1, S2 |
| Agent | G |
| Target project | Project B |
| New licence | `license: Apache-2.0` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Skill publish** | | |
| 1 | Publish S1 with the publish wizard | S1 is published |
| 2 | Open the published S1 in the Catalog in **Edit** mode and export it | The frontmatter and the export contain `license`, `compatibility`, `allowed-tools`, `argument-hint`, the `metadata` keys, tags and run settings, the same as the source export |
| 3 | Change the licence of S1 to the new licence and publish again | The Catalog copy shows the new licence |
| **Agent export / import** | | |
| 4 | Export agent G as Markdown | Each embedded skill has a `frontmatter:` block with its licence, extra keys, tags and run settings |
| 5 | Open Agents → **Add** → **Import from file**, choose the Markdown file, select Project B in **Import parameters** and click **Import**. In **Import Complete** click **Got it**, then open each recreated skill | All frontmatter values are restored |
| **Agent publish** | | |
| 6 | Publish agent G and open its skills in the Catalog | S1 and S2 keep their frontmatter |
| 7 | Change the licence of S2 and publish agent G again | The Catalog copy of S2 shows the new licence |
| **Fork** | | |
| 8 | Fork S1 into Project B, then fork the published agent G into Project B | The forked skills keep the licence, extra keys, tags and run settings |

---

## Expected Final State

All copies of S1 and S2 keep their frontmatter. Unpublish and delete the test entities after the run.

---

## Pass/Fail Criteria

**Pass:**
- The licence, extra keys, tags and run settings are kept in every published, imported and forked copy.
- Licence changes reach the Catalog copy after republishing.

**Fail:**
- Any key or value is missing or different in a copy.
- A licence change does not reach the Catalog copy.

---

## Notes

- Adds frontmatter checks to the flows covered by ELITEA-2595, ELITEA-2600, ELITEA-2602, ELITEA-1794 and ELITEA-1795.
- With skills that have files, agent G exports as `.agent.zip` instead. That case is covered by ELITEA-4921.

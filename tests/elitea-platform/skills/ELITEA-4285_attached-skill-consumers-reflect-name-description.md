---
id: ELITEA-4285
title: "Verify attached-Skill consumers in Agent config and Chat mention continue to reflect Name/Description correctly"
priority: high
type: integration
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Editor or Admin role
- An Agent has at least one Skill attached
- A Chat conversation has access to that Agent/Skill

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| New Skill Name (via frontmatter) | `renamed-attached-skill` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent configuration | Attached Skill displays its current Name and Description correctly |
| 2 | Edit the Skill's Name via the frontmatter (not the field) and save; reopen the Agent configuration | Updated name is reflected in the Agent configuration |
| 3 | In a Chat conversation, type `~` to trigger the Skill mention autocomplete | Skill's updated name/description appear correctly in the list |
| 4 | Invoke the Skill via `~mention` | Skill loads and executes using the correct (non-frontmatter-containing) Instructions body |

## Expected Final State

Agent configuration and Chat `~mention` autocomplete consistently reflect the Skill's current Name/Description, including when changed via the frontmatter, with no change to execution behavior.

## Pass/Fail Criteria

**Pass:**
- Agent config reflects the Skill's current Name/Description after a frontmatter-driven rename
- Chat `~mention` list and invocation reflect the updated Skill correctly

**Fail:**
- Agent config or Chat mention shows stale or incorrect Name/Description
- Skill invocation behaves incorrectly or includes frontmatter content in execution

---
id: ELITEA-4768
title: "Open in new tab: Entity cards open the correct entity"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, card-view, agents, pipelines, skills, toolkits, mcps, credentials, applications, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4768: Open in new tab: Entity cards open the correct entity

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that entity cards in card view are real links and "Open link in new tab" opens the configuration page of the clicked entity for each entity type.

**Coverage:**
- Card view for Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Credentials, Applications
- Correct entity is opened (name/ID)
- Original list state is preserved

## Preconditions
- User is logged in and has access to a project.
- At least one entity of each type exists in the project: Agent, Pipeline, Skill, Toolkit, MCP, Credential, Application.
- Card view is selected on each entity list page.

## Test Data
- One entity per type with a known name (e.g., `QA-Agent-NewTab`, `QA-Pipeline-NewTab`, …)

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Agents** list (card view); right-click an agent card and select "Open link in new tab" | Native menu shows the option; new tab opens that agent's configuration page |
| 2 | In the new tab, check the entity name and the ID in the URL | Name and ID match the clicked agent; page loads without errors |
| 3 | Open **Pipelines** list; right-click a pipeline card → "Open link in new tab" | New tab opens that pipeline's configuration page with matching name/ID |
| 4 | Open **Skills** list; right-click a skill card → "Open link in new tab" | New tab opens that skill with matching name/ID |
| 5 | Open **Toolkits & Indexes** list; right-click a toolkit card → "Open link in new tab" | New tab opens that toolkit with matching name/ID |
| 6 | Open **MCPs** list; right-click an MCP card → "Open link in new tab" | New tab opens that MCP with matching name/ID |
| 7 | Open **Credentials** list; right-click a credential card → "Open link in new tab" | New tab opens that credential with matching name/ID |
| 8 | Open **Applications** list; right-click an application card → "Open link in new tab" | New tab opens that application with matching name/ID |
| 9 | Before one of the above, apply a search/filter and scroll the list; then open a card in a new tab and return to the original tab | Original tab keeps the same filter, search, and scroll position |

## Expected Final State
Each entity type's card opens its own entity in a new tab; the list in the original tab is unchanged.

## Pass/Fail Criteria
- **Pass:** All 7 card types open the correct entity in a new tab and the original list is unchanged.
- **Fail:** Any card type lacks the option, opens a wrong/empty entity, errors on load, or resets the original list.

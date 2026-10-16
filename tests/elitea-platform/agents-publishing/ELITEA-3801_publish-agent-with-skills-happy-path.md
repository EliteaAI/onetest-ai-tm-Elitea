---
id: ELITEA-3801
title: "Publish agent with skills - happy path"
priority: critical
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with `models.applications.publish.post` permission
- Agent created with valid name, description, instructions, tags, custom icon
- 3 Skills with valid content attached (well-formed instructions 100+ chars, no placeholders)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Code Assistant with Skills" |
| Skill 1 | "Code Review Helper" - code review instructions |
| Skill 2 | "Documentation Writer" - doc writing guidelines |
| Skill 3 | "Test Generator" - test generation rules |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open test agent with 3 attached Skills | Agent configuration loads; Skills section shows 3/5 skills |
| 2 | Click three-dot menu (⋮) in agent tab bar | Context menu opens |
| 3 | Click **Publish** | Publish wizard modal opens on Preparation step |
| 4 | Verify step indicators | Shows: `Preparation → Validation → Publishing` with Preparation active |
| 5 | Enter version name: "1.0.0" | Field accepts input |
| 6 | Select category from dropdown | Category selected |
| 7 | Expand Publishing Terms section | Terms content visible |
| 8 | Verify Skills mentioned as retained (not excluded) | Skills listed under retained content alongside sub-agents and internal tools |
| 9 | Check "I agree with Publishing Terms" checkbox | Checkbox checked |
| 10 | Click **Continue** | Validation step activates; spinner shows "Reviewing your agent version..." |
| 11 | Wait for validation to complete | Step indicator changes to **Publishing** (green badge) |
| 12 | Verify severity counters | Critical: 0, Warnings: 0 (or minimal), Suggestions: may have some |
| 13 | Verify no Skills-related critical/warning issues | No findings with `context: skill:` at critical/warning level |
| 14 | Click **Copy** button on validation toolbar | Validation report copied to clipboard |
| 15 | Verify copied report format | Report contains structured validation results |
| 16 | Click **Full-screen** button | Validation Details dialog opens |
| 17 | Verify full-screen shows complete results | All findings visible; can expand/collapse |
| 18 | Close full-screen dialog | Return to wizard |
| 19 | Verify **Publish** button is enabled | Button clickable |
| 20 | Click **Publish** | Shows "Publishing your agent..."; then toast: "The agent has been published" |
| 21 | Verify wizard closes | Modal dismissed |
| 22 | Verify published version | Published version appears in agents version dropdown and has "book" icon |
| 23 | Navigate to **Agent Hub/Catalog** | Agent Hub page loads |
| 24 | Search for "Code Assistant with Skills" | Agent appears in search results as card |
| 25 | Switch to skills and search for "Code Review Helper" (Skill name) | **No independent Skill card appears** |
| 26 | Search for "Documentation Writer" | **No independent Skill card appears** |
| 27 | Search for "Test Generator" | **No independent Skill card appears** |
| 28 | Filter Agent Hub by the selected category | Published agent appears in filtered results; no Skills appear |
| 29 | Click on published agent card | Agent detail/preview opens |
| 30 | Click "Add to conversation" or start chat | Agent added to conversation |
| 31 | Test agent with prompt that triggers Skill functionality | Agent responds using Skill instructions (Skills functionally attached) |
| 32 | Verify all 3 Skills work in conversation | Each Skill's behavior accessible |

## Expected Final State

Agent is published successfully with all 3 attached Skills embedded in the snapshot. Skills are NOT discoverable as independent entities in Agent Hub. Published agent retains full Skill functionality in conversations.

## Pass/Fail Criteria

**Pass:**
- All 3 attached Skills embedded in published snapshot
- Validation UI fully functional (copy, full-screen, expand/collapse)
- Publishing Terms mention Skills as retained
- Agent publishes successfully
- Skills NOT discoverable as independent entities in Agent Hub
- Published agent retains full Skill functionality

**Fail:**
- Skills missing from published snapshot
- Skills appear as independent entities in Agent Hub
- Validation fails unexpectedly for valid Skills
- Published agent loses Skill functionality

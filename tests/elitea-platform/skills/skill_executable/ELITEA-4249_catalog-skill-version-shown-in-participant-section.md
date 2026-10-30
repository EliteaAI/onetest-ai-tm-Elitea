---
id: ELITEA-4249
title: Catalog skill participant shows version information
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, catalog, chat, participant, versioning, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4249: Catalog skill participant shows version information

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Catalog skill participant displays version information in the chat's participant section.

**Coverage:**
- Skill shows in SKILLS participant section
- Version is displayed (e.g., "Catalog v8")
- Skill name and icon visible
- Source shown as "Catalog"

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant is open
- Catalog skill has published versions (e.g., "animal-joke v8")

## Test Data

- Catalog skill: "animal-joke" with version "v8" (or any published skill with version)
- Expected: Skill shown as "animal-j... Catalog v8" or similar

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create chat with Catalog skill (e.g., "animal-joke") via Run button | Chat opens with skill participant |
| 2 | Observe right panel "PARTICIPANTS" section | Right panel displays participants |
| 3 | Look for "SKILLS" subsection under participants | "SKILLS" section is visible |
| 4 | Check the skill participant display | Skill appears with name, icon, and version label |
| 5 | Verify skill name is displayed | Skill name "animal-j..." or full name "animal-joke" is visible |
| 6 | Verify version is displayed | Version label shows "Catalog v8" (or current version) |
| 7 | Verify skill icon is displayed | Skill's icon/avatar is visible |
| 8 | Verify source is shown as "Catalog" | Label indicates skill is from Catalog (not user's own skill) |
| 9 | (Optional) Hover over skill to see full details | Tooltip or expanded view shows full skill name and version |
| 10 | Compare with screenshot from #6922 issue | Display matches expected format from requirements |

## Expected Final State

Skill participant shows in SKILLS section with name, icon, version (e.g., "Catalog v8"), and Catalog source.

## Pass/Fail Criteria

**Pass:** Skill displayed in SKILLS section with name, icon, version label, and Catalog source indicator.

**Fail:** Missing version info, incorrect display, or skill not shown in participant section.

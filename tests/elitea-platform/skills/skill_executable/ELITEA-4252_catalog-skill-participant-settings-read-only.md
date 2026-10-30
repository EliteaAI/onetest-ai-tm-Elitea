---
id: ELITEA-4252
title: Catalog skill participant settings are read-only in chat
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, catalog, chat, read-only, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4252: Catalog skill participant settings are read-only in chat

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Catalog skill participant's instructions and settings are read-only; user cannot modify published skill configuration.

**Coverage:**
- Skill instructions visible but not editable
- User cannot modify published skill
- Model override allowed (per chat only, not saved)
- Skill configuration locked

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant is open
- Skill has published instructions and settings

## Test Data

- Catalog skill: Any published skill with instructions
- Expected: Instructions read-only, no edit capability

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat with Catalog skill participant | Chat displays with skill in SKILLS section |
| 2 | Click on the skill participant in right panel | Skill details expand or show in panel |
| 3 | Observe the skill instructions display | Instructions are visible and readable |
| 4 | Try to click or edit the instructions text | Instructions are read-only, no edit cursor or input field |
| 5 | Look for "Edit" button or icon near instructions | NO "Edit" button present for Catalog skills |
| 6 | Check if model settings can be modified permanently | Model can be overridden for current chat only (per ELITEA-4246) |
| 7 | Verify no "Save" button for skill configuration | No way to save changes to published skill configuration |
| 8 | Compare with user's own skills in chat | User's own skills might have edit capability, but Catalog skills do not |
| 9 | Verify skill source shows "Catalog" | Label indicates skill is from Catalog (not owned by user) |
| 10 | Confirm only skill owner can modify published skill | Only skill publisher/owner can edit published skill configuration |

## Expected Final State

Catalog skill instructions and settings are read-only; user cannot modify; only model override per chat allowed.

## Pass/Fail Criteria

**Pass:** Skill instructions read-only, no edit capability, model override per chat only, configuration locked.

**Fail:** User can edit Catalog skill instructions or permanently modify published skill settings.

## Notes

This test ensures published Catalog skills remain secure and consistent. Only the skill owner can modify published skill configuration. Users can only override model per chat session (temporary, not saved to skill).

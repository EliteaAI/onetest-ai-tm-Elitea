---
id: ELITEA-4181
title: "Verify immutability error is displayed when attempting to edit published version's run_settings"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill with run_settings configured exists and is PUBLISHED
- User has permission to view published skills

## Test Data

| Field | Value |
|-------|-------|
| Skill status | Published |
| Original model | GPT-4 Turbo |
| Original reasoning | Medium |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to published skill details page | Skill details displayed, status shows "Published" |
| 2 | Expand "Run settings" accordion | Run settings section displays |
| 3 | Verify Model field is displayed as read-only (no dropdown, greyed out or locked icon) | Model field read-only |
| 4 | Verify Model settings icon is disabled or not present | Settings icon disabled |
| 5 | Verify "Include project context" toggle is disabled | Toggle is read-only |
| 6 | Attempt to click on any run_settings field | No interaction possible, fields are locked |
| 7 | If edit is somehow attempted (via API or edge case), observe error | Error displayed: "Published versions cannot be modified" or similar immutability error |
| 8 | Verify "Save" button is disabled or not present for published version | Save disabled |

## Expected Final State

- Published version's run_settings are completely read-only
- No edits possible through UI or API
- Clear visual indication that fields are locked

## Pass/Fail Criteria

**Pass:**
- All run_settings fields are read-only for published versions
- Immutability error displayed if edit attempted
- Visual indicators show locked state
- Published version remains unchanged

**Fail:**
- Run_settings fields are editable for published versions
- No immutability error when edit attempted
- Published version can be modified
- No visual indication of read-only state

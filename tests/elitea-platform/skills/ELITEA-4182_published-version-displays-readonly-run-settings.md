---
id: ELITEA-4182
title: "Verify published skill version displays Run settings section as read-only"
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
- A published skill with configured run_settings exists

## Test Data

| Field | Value |
|-------|-------|
| Skill | Any published skill with run_settings |
| Status | Published |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to published skill details | Skill page opens |
| 2 | Verify skill status badge shows "Published" | Status: Published |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Verify Model field shows value but is not clickable/editable | Model displayed as text, no dropdown |
| 5 | Verify Model settings icon is greyed out or hidden | Settings icon disabled |
| 6 | Verify "Include project context" toggle is greyed out and not clickable | Toggle disabled |
| 7 | Hover over disabled fields → Verify tooltip or visual feedback | Tooltip: "Published versions are read-only" or similar |
| 8 | Verify no "Save" or "Update" button is available for run_settings | Edit controls hidden |

## Expected Final State

- All run_settings fields display as read-only
- Clear visual distinction between editable and published versions
- Helper text or tooltips explain immutability

## Pass/Fail Criteria

**Pass:**
- All run_settings fields are visually read-only
- No edit controls available
- Tooltips explain why fields are disabled
- Published version cannot be modified

**Fail:**
- Any run_settings field appears editable
- No visual indication of read-only state
- User can click or interact with fields
- No explanation for disabled state

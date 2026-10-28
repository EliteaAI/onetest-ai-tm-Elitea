---
id: ELITEA-4196
title: "Verify catalog user attempting to edit published skill run_settings is rejected and must fork first"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User A (skill author) has published a skill to catalog with run_settings
- User B (catalog consumer) is logged in to `{{base_url}}`
- User B has view access to catalog but NOT edit access to User A's skill

## Test Data

| Field | Value |
|-------|-------|
| Published skill | Catalog skill with run_settings |
| User A | Skill owner |
| User B | Catalog consumer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | User B: Navigate to catalog → Find published skill | Skill found |
| 2 | User B: Open skill details | Skill details displayed |
| 3 | User B: Expand "Run settings" accordion | Run settings displayed (read-only) |
| 4 | User B: Verify all run_settings fields are read-only | Fields greyed out, no edit controls |
| 5 | User B: Attempt to click Model selector → Verify not clickable | Model field disabled |
| 6 | User B: Attempt to edit any run_settings field (via UI or API) | Edit blocked |
| 7 | Observe error message or disabled state | Error: "Published skills from catalog are read-only. Fork to create your own editable copy" or similar |
| 8 | User B: Click "Fork" button | Fork dialog opens |
| 9 | User B: Complete fork operation | Skill forked to User B's project |
| 10 | User B: Navigate to forked skill → Expand "Run settings" | Run settings displayed (now editable) |
| 11 | User B: Verify forked skill's run_settings are editable | All fields editable |
| 12 | User B: Change model or settings → Save | Changes saved successfully |

## Expected Final State

- Catalog user cannot edit published skill run_settings
- Clear guidance to fork for editing
- Forked skill is fully editable with preserved run_settings
- Catalog skill remains unchanged

## Pass/Fail Criteria

**Pass:**
- Published skill run_settings read-only for catalog users
- Edit attempts blocked or disabled
- Clear error message or guidance to fork
- Fork operation preserves run_settings
- Forked skill is fully editable

**Fail:**
- Catalog user can edit published skill run_settings
- No error message when edit attempted
- Fork operation loses run_settings
- Forked skill is not editable

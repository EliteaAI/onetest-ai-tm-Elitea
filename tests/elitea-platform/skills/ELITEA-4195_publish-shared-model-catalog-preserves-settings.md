---
id: ELITEA-4195
title: "Verify skill with shared model and reasoning settings publishes successfully and catalog user runs preserve settings"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User A (skill author) is logged in to `{{base_url}}`
- User A has permission to publish skills
- A shared/public model exists (e.g., Claude Opus from public project)
- User B (catalog consumer) has access to catalog

## Test Data

| Field | Value |
|-------|-------|
| Skill | Skill with run_settings |
| Model | Shared/public Claude Opus |
| Reasoning | High |
| Max tokens | 8000 |
| Context | OFF |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | User A: Create skill → Configure run_settings with shared model (Claude Opus), Reasoning: High, Max tokens: 8000, Context: OFF | Skill configured |
| 2 | User A: Click "Publish" | Publish validation starts |
| 3 | User A: Complete publish flow | Skill published successfully to catalog |
| 4 | User A: Navigate to catalog → Verify skill appears | Skill in catalog |
| 5 | User B: Log in to `{{base_url}}` (different user/project) | User B logged in |
| 6 | User B: Navigate to catalog → Find published skill | Skill found in catalog |
| 7 | User B: View skill details → Expand "Run settings" (read-only) | Run settings displayed |
| 8 | User B: Verify Model: Claude Opus, Reasoning: High, Max tokens: 8000, Context: OFF | Settings preserved |
| 9 | User B: Run skill from catalog | Skill execution starts |
| 10 | User B: Wait for completion → Check execution used Claude Opus with High reasoning | Execution used published settings |
| 11 | User B: Verify API response confirms correct model and settings | Response metadata matches published settings |

## Expected Final State

- Skill publishes successfully with shared model
- Published skill appears in catalog with run_settings
- Catalog user can view run_settings (read-only)
- Catalog user's execution uses published settings
- All run_settings preserved end-to-end

## Pass/Fail Criteria

**Pass:**
- Publish succeeds with shared model
- Skill appears in catalog
- Run_settings preserved and visible in catalog
- Catalog user execution uses published model and settings
- No settings lost during publish/catalog flow

**Fail:**
- Publish fails with shared model
- Run_settings not preserved in catalog
- Catalog user cannot see run_settings
- Execution uses different model or settings
- Settings lost or overridden

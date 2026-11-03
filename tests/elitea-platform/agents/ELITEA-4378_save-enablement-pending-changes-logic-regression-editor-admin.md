---
id: ELITEA-4378
title: "Save-Enablement (Pending-Changes) Logic Still Correct for Editor and Admin on Agent Details (Regression)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- Editor and Admin accounts with access to a test Agent
- Agent starts with no pending changes (Save disabled, Discard disabled)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Roles | Editor, Admin |
| Agent | Any existing agent accessible to both roles |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as Editor. Open the test Agent with no pending changes. | Save: disabled. Discard: disabled. |
| 2 | Make a field edit (e.g. instructions text), then revert it back to the exact original value without saving. | Save and Discard return to disabled once the content matches the last-saved state (no false-positive enabling for a net-zero change). |
| 3 | Make a genuine field edit and leave it unreverted. | Save and Discard become enabled (no false-negative — a real pending change correctly enables the controls). |
| 4 | Click Save. | Change persists; Save and Discard return to disabled afterward (no pending changes remain). |
| 5 | Repeat steps 1–4 for a different field type if available (e.g. a toolkit/tool configuration change) to confirm the pending-changes detection is not limited to text fields. | Same enable/disable behavior holds for the additional field type. |
| 6 | Repeat steps 1–5 logged in as Admin. | Identical results to Editor — pending-changes detection logic is unaffected by the Viewer-targeted fix. |

## Expected Final State

Save and Discard enablement for Editor and Admin continues to accurately reflect whether there is a genuine, unsaved pending change, with no false positives or false negatives introduced by this fix.

## Pass/Fail Criteria

**Pass:**
- Save/Discard remain disabled when no net change exists (including after an edit-then-revert)
- Save/Discard become enabled only when a genuine pending change exists
- Behavior is identical for both Editor and Admin, and unchanged from pre-fix baseline

**Fail:**
- Save or Discard is enabled when there is no genuine pending change (false positive)
- Save or Discard remains disabled despite a genuine pending change (false negative)
- Any difference in this behavior is observed between Editor and Admin

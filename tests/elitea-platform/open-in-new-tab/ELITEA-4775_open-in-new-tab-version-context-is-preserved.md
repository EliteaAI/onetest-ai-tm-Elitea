---
id: ELITEA-4775
title: "Open in new tab: Version context is preserved"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, versions, run-history, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4775: Open in new tab: Version context is preserved

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an entity is opened in a new tab from a non-base version, the same version is selected in the new tab (entity page and Run History).

**Coverage:**
- Agent and Pipeline non-base versions
- Entity page and Run History
- Refresh of the new tab

## Preconditions
- User is logged in.
- An Agent and a Pipeline each have at least one saved non-base version (e.g., `v2`).

## Test Data
- Agent `QA-Agent-NewTab` with version `v2`; Pipeline `QA-Pipeline-NewTab` with version `v2`

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent and select version `v2` | `v2` is selected |
| 2 | Open the agent card/link for this version in a new tab | New tab opens the agent with `v2` selected |
| 3 | With `v2` selected, open **Run History** from the three-dot menu in a new tab | Run History for `v2` is shown |
| 4 | Refresh both new tabs | `v2` remains selected in both |
| 5 | Repeat steps 1–4 for the **Pipeline** | Same result for the pipeline's `v2` |

## Expected Final State
Non-base version context carries over to new tabs and survives refresh.

## Pass/Fail Criteria
- **Pass:** The non-base version is selected in every new tab, including after refresh.
- **Fail:** The new tab falls back to the base/latest version.

## Notes
- The version dropdown items themselves lacking "Open link in new tab" is tracked separately in EliteaAI/elitea_issues#7640.

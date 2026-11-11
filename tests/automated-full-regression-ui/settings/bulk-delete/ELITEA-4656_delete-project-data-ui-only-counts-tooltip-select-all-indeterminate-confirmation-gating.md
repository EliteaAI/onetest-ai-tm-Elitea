---
id: ELITEA-4656
title: "Delete Project Data section renders correctly at the bottom of Settings General with accurate counts, present tooltip, and correct confirmation-gating (UI-only, no deletion performed)"
priority: high
type: functional
module: bulk-delete
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189]
---

# ELITEA-4656: Delete Project Data — UI-Only Verification (No Deletion Performed)

## Preconditions

- Logged in to `{{base_url}}` as a private-project owner or team-project Admin
- Project has a known, non-zero number of Agents (used as the count cross-check)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |
| Checkbox set | Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials |
| Invalid confirmation values | `delete`, `DELET` |
| Valid confirmation value | `DELETE` |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → General and scroll to the bottom of the page | "Delete Project Data" section appears below "Back Up & Restore", as the last section on the page |
| 2 | Inspect the section's checkboxes | A checkbox exists for each of: Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, plus a separate "Select all" checkbox |
| 3 | Independently note the real number of Agents via the Agents list page, then compare against the count shown next to the Agents checkbox | The two numbers match |
| 4 | Hover over (or click, per the UI's trigger) the info icon next to Credentials | A tooltip is present and displays text |
| 5 | With no checkboxes selected, inspect "Select all" | Shown fully unchecked |
| 6 | Select two or more entity-type checkboxes individually, leaving at least one unselected | "Select all" renders in its indeterminate state (dash/"-"), not fully checked or fully unchecked |
| 7 | Select every remaining checkbox so all types are checked | "Select all" now renders fully checked |
| 8 | Click "Delete selected data" (or equivalent) to open the confirmation modal | Modal opens |
| 9 | Observe the "Delete permanently" (or equivalent) button immediately after the modal opens, before typing anything | Button is disabled |
| 10 | Type a value other than the exact case-sensitive "DELETE" (e.g. "delete" or "DELET") | Button remains disabled |
| 11 | Type the exact case-sensitive "DELETE" | Button becomes enabled |
| 12 | Without clicking the now-enabled button, close/cancel the modal, then reload Settings → General | All entity-type counts are unchanged from step 2/3; no deletion occurred |

## Expected Final State

The Delete Project Data section is correctly positioned, fully populated, shows accurate counts and a working Credentials tooltip, the "Select all" checkbox correctly reflects partial vs full selection, and the destructive action remains gated behind an exact "DELETE" confirmation. No data in the project is deleted during this check.

## Pass/Fail Criteria

**Pass:**
- Section position, checkbox set, and Agents count are all correct
- Credentials tooltip is present
- "Select all" shows indeterminate state for a partial selection and fully checked for all selected
- "Delete permanently" stays disabled until the exact "DELETE" text is typed
- No deletion occurs and counts are unchanged after cancelling

**Fail:**
- Section is missing, misplaced, or missing a checkbox/tooltip
- Displayed Agents count does not match the real count
- "Select all" fails to show the indeterminate state for a partial selection
- The confirmation button enables with an incorrect value, or any deletion occurs despite the modal being cancelled

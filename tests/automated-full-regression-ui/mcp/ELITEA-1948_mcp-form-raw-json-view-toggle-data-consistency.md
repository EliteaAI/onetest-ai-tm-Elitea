---
id: ELITEA-1948
title: "MCP Form/Raw JSON View Toggle — Data Consistency"
priority: medium
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_form_raw_json_view_sync.TestMcpFormRawJsonViewSync.test_form_raw_json_view_sync_and_discard
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1744
---

# ELITEA-1948: MCP Form/Raw JSON View Toggle — Data Consistency

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that toggling between Form and Raw JSON views on a Remote MCP detail page maintains data consistency, and that unsaved changes made in one view are reflected in the other and reverted correctly on Discard.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Note all field values: Toolkit Name, Description, Url, Timeout, Cache TTL, Enable Caching, Ssl Verify | Current values are observed |
| 3 | Click "Raw Json" toggle button | JSON editor is displayed |
| 4 | Verify JSON editor shows matching values: name matches Toolkit Name, description matches, settings.url matches, settings.timeout matches, etc. | JSON values match Form values |
| 5 | Modify description value in Raw Json view | JSON editor shows the updated description |
| 6 | Click "Form" toggle (without saving) | Form view is displayed |
| 7 | Verify Form view shows the updated description | Description field reflects the change |
| 8 | Click "Raw Json" again — verify JSON still has the modification | JSON retains the unsaved change |
| 9 | Click Discard — verify both views revert | Both Form and Raw JSON views show original values |

---

## Expected Final State

After Discard, both Form and Raw JSON views display the original values without any unsaved modifications.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Data is consistent between views; Discard reverts changes in both.

**Fail:**
- Any step produces an error or unexpected result.
- Views show inconsistent data, or Discard does not revert changes in one or both views.

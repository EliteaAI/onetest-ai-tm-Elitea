---
id: ELITEA-1949
title: "MCP Type Selection — Local vs Remote Display"
priority: medium
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_type_picker_local_vs_remote.TestMcpTypePickerLocalVsRemote.test_type_picker_sections_documentation_link_and_filters
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1744
---

# ELITEA-1949: MCP Type Selection — Local vs Remote Display

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the MCP type selection page correctly displays Local and Remote sections with appropriate content, a working Documentation link, and type filter buttons that control section visibility.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has navigated to the MCP creation page (/app/mcps/create).

---

## Test Data

| Field | Value |
|-------|-------|
| Documentation link | https://docs.elitea.ai/integrations/mcp/create-and-use-server-stdio |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP creation page (/app/mcps/create) | Page loads at the correct URL |
| 2 | Verify page heading "Choose the MCP type" is displayed | Heading is visible |
| 3 | Verify Local section shows message: "Still no local MCP available. Follow creation guides in our Documentation." | Local section displays the correct message |
| 4 | Verify "Documentation" is a clickable link pointing to https://docs.elitea.ai/integrations/mcp/create-and-use-server-stdio | Link is present and points to the correct URL |
| 5 | Verify Remote section shows "Remote MCP" card with icon | Remote MCP card is visible |
| 6 | Verify type filter buttons "Local" and "Remote" are present | Both filter buttons are shown |
| 7 | Click "Local" filter — verify only Local section content shown | Only Local section is visible |
| 8 | Click "Remote" filter — verify only Remote section content shown | Only Remote section is visible |

---

## Expected Final State

The Remote filter shows only the Remote MCP card; the Local section is hidden.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both sections display correctly; Documentation link points to the right URL; filters work.

**Fail:**
- Any step produces an error or unexpected result.
- Sections display wrong content, Documentation link is broken, or filters have no effect.

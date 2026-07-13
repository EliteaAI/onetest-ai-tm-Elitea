---
id: ELITEA-1959
title: "Remote MCP — Copy Link from Three-Dot Menu"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1959: Remote MCP — Copy Link from Three-Dot Menu

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Copy link" action in the three-dot menu copies a valid URL to the clipboard, and that navigating to the copied URL opens the same MCP detail page.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP detail page is open.

---

## Test Data

| Field | Value |
|-------|-------|
| Expected URL format | https://dev.elitea.ai/app/mcps/all/{id}?viewMode=owner&name={MCP name} |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page | Detail page loads |
| 2 | Click three-dot menu | Menu opens |
| 3 | Click "Copy link" | Copy action is triggered |
| 4 | Verify clipboard contains the MCP URL (e.g., https://dev.elitea.ai/app/mcps/all/208?viewMode=owner&name=Web%20Search) | Clipboard contains the correct MCP URL |
| 5 | Open a new browser tab and paste the URL | URL is pasted in the address bar |
| 6 | Verify the same MCP detail page loads correctly | MCP detail page loads for the correct MCP |

---

## Expected Final State

The copied URL navigates to the same MCP detail page when opened in a new browser tab.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Copied URL is valid and loads the correct MCP detail page.

**Fail:**
- Any step produces an error or unexpected result.
- Clipboard does not contain the URL, or the URL does not load the correct page.

---
id: ELITEA-1926
title: "Edit Remote MCP — Change URL"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1926: Edit Remote MCP — Change URL

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Remote MCP's URL can be updated, saved, and confirmed in both the Form view and the Raw JSON view after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.

---

## Test Data

| Field | Value |
|-------|-------|
| New URL | https://new-mcp-server.example.com/sse |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Note current URL value in the "Url *" field | Current URL is observed |
| 3 | Clear the URL field and enter a new URL "https://new-mcp-server.example.com/sse" | Field displays the new URL |
| 4 | Verify Save button becomes enabled | Save button is clickable |
| 5 | Click Save | Operation completes successfully |
| 6 | Reload page — verify new URL value persisted in "Url *" field | Field shows "https://new-mcp-server.example.com/sse" |
| 7 | Switch to Raw Json view — verify "url" field in JSON matches new value | JSON "url" field shows the updated URL |

---

## Expected Final State

The MCP URL is updated, saved, and confirmed in both Form and Raw JSON views after a page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- New URL is persisted and visible in both views after reload.

**Fail:**
- Any step produces an error or unexpected result.
- URL is not persisted or Raw JSON does not reflect the change.

---
id: ELITEA-4759
title: "Regression - MCP test: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast"
priority: critical
type: regression
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:chat, feat:mcp, r-2.0.9, automated:UI:regression]
requirements: ["EliteaAI/elitea_issues#5838"]
---

# ELITEA-4759: Regression - MCP test: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast

**Module:** mcp-servers · **Priority:** critical · **Type:** regression

**Objective:** MCP test: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast.

Manual source: ELITEA-4753

---

## Preconditions

- User is logged in to {{base_url}} in a project where they can edit entities (e.g. **Bugs & Features**).
- An MCP toolkit exists and is connected (e.g. **test** / Epam Onehub Core, banner **Connected!**) with tools loaded.

---

## Test Data

| Field | Value |
|-------|-------|
| MCP | connected MCP, e.g. test (Epam Onehub Core) |
| Tool | Current user id |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the MCP (from **MCPs** or **Toolkits & Indexes**) | MCP page opens with **Connected!** banner; **Test** button is visible. |
| 2 | Click **Test** | **Test Toolkit** page opens with the MCP tool list on the left. |
| 3 | Select a tool (e.g. **Current user id**) | Tool and **Model** fields are shown; **Run Test** is visible. |
| 4 | Click **Run Test** | Result card appears with `current_user_id` and the returned value. |
| 5 | Observe the icons below the result card | **Copy markdown** (M icon) and **Copy text** (copy icon) are visible. |
| 6 | Hover the **M** icon in the result card toolbar | Tooltip **Copy markdown** is shown. |
| 7 | Click **Copy markdown** | Icon is clickable; confirmation toast **Markdown copied to clipboard.** appears. |
| 8 | Hover the copy icon next to it in the result card toolbar | Tooltip **Copy text** is shown. |
| 9 | Click **Copy text** | Icon is clickable; confirmation toast **Text copied to clipboard.** appears. |

---

## Expected Final State

Copy markdown and Copy text icons are available under the MCP test result and each click is confirmed by a toast.

---

## Pass/Fail Criteria

**Pass:**
- **Copy markdown** and **Copy text** icons are visible and clickable.
- After each click a confirmation toast appears.

**Fail:**
- Either icon is missing or not clickable.
- No confirmation toast appears after clicking.

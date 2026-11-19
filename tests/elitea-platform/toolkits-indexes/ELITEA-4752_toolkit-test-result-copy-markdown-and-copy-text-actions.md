---
id: ELITEA-4752
title: "Toolkit test: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:chat, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#5838"]
---

# ELITEA-4752: Toolkit test: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast

**Module:** toolkits-indexes · **Priority:** critical · **Type:** functional

**Objective:** Toolkit test: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast.

---

## Preconditions

- User is logged in to {{base_url}} in a project where they can edit entities (e.g. **Bugs & Features**).
- An **Artifact** toolkit exists (e.g. **alita**) with at least one enabled read tool.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Artifact toolkit, e.g. alita |
| Tool | List files (parameters left default) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Toolkits & Indexes** and open the Artifact toolkit | Toolkit page opens; **Test** and **Run History** buttons are visible. |
| 2 | Click **Test** | **Test Toolkit** page opens: Test Settings with tool list on the left, Results on the right. |
| 3 | Select a tool (e.g. **List files**) | Tool parameters and **Model** are shown; **Run Test** button is visible. |
| 4 | Click **Run Test** | Result card appears under Results with `list_files` and JSON output. |
| 5 | Observe the icons below the result card | **Copy markdown** (M icon) and **Copy text** (copy icon) are visible. |
| 6 | Hover the **M** icon in the result card toolbar | Tooltip **Copy markdown** is shown. |
| 7 | Click **Copy markdown** | Icon is clickable; confirmation toast **Markdown copied to clipboard.** appears. |
| 8 | Hover the copy icon next to it in the result card toolbar | Tooltip **Copy text** is shown. |
| 9 | Click **Copy text** | Icon is clickable; confirmation toast **Text copied to clipboard.** appears. |

---

## Expected Final State

Copy markdown and Copy text icons are available under the toolkit test result and each click is confirmed by a toast.

---

## Pass/Fail Criteria

**Pass:**
- **Copy markdown** and **Copy text** icons are visible and clickable.
- After each click a confirmation toast appears.

**Fail:**
- Either icon is missing or not clickable.
- No confirmation toast appears after clicking.

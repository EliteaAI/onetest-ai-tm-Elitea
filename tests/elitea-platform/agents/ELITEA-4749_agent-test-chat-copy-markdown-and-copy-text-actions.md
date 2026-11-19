---
id: ELITEA-4749
title: "Agent test chat: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:chat, feat:agents, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#5838"]
---

# ELITEA-4749: Agent test chat: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Agent test chat: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast.

---

## Preconditions

- User is logged in to {{base_url}} in a project where they can edit entities (e.g. **Bugs & Features**).
- An agent exists (e.g. **Fairy Tale File Creator**) with an LLM model selected.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | any existing agent, e.g. Fairy Tale File Creator |
| Request | any request, e.g. `Create a fairy tale about a dragon who is afraid of flying.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Agents** in the left menu and open the agent | Agent configuration page opens; **Test Agent** button is visible. |
| 2 | Click **Test Agent** | Test chat panel opens on the right with the welcome message and an input box. |
| 3 | Enter the request from Test Data and click the send arrow | Agent response is generated. |
| 4 | Observe the icons below the agent response | **Copy markdown** (M icon) and **Copy text** (copy icon) are visible. |
| 5 | Hover the **M** icon in the agent response toolbar | Tooltip **Copy markdown** is shown. |
| 6 | Click **Copy markdown** | Icon is clickable; confirmation toast **Markdown copied to clipboard.** appears. |
| 7 | Hover the copy icon next to it in the agent response toolbar | Tooltip **Copy text** is shown. |
| 8 | Click **Copy text** | Icon is clickable; confirmation toast **Text copied to clipboard.** appears. |

---

## Expected Final State

Copy markdown and Copy text icons are available under the agent response and each click is confirmed by a toast.

---

## Pass/Fail Criteria

**Pass:**
- **Copy markdown** and **Copy text** icons are visible and clickable.
- After each click a confirmation toast appears.

**Fail:**
- Either icon is missing or not clickable.
- No confirmation toast appears after clicking.

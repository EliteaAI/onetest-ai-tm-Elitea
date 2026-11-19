---
id: ELITEA-4760
title: "Regression - Test chat: user message Copy markdown and Copy text icons are visible, clickable and confirmed by a toast"
priority: high
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9, automated:UI:regression]
requirements: ["EliteaAI/elitea_issues#5838"]
---

# ELITEA-4760: Regression - Test chat: user message Copy markdown and Copy text icons are visible, clickable and confirmed by a toast

**Module:** chat-interface · **Priority:** high · **Type:** regression

**Objective:** Test chat: user message Copy markdown and Copy text icons are visible, clickable and confirmed by a toast.

Manual source: ELITEA-4754

---

## Preconditions

- User is logged in to {{base_url}} in a project where they can edit entities (e.g. **Bugs & Features**).
- An agent or skill exists to open its test chat.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | any text, e.g. `Create a fairy tale about a dragon.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an agent and click **Test Agent** (or a skill and click **Test**) | Test chat panel opens. |
| 2 | Enter the message from Test Data and click the send arrow | User message appears at the top with sender name and timestamp. |
| 3 | Observe the icons below the user message | **Copy markdown** (M icon) and **Copy text** (copy icon) are visible. |
| 4 | Click **Copy markdown** | Icon is clickable; confirmation toast **Markdown copied to clipboard.** appears. |
| 5 | Click **Copy text** | Icon is clickable; confirmation toast **Text copied to clipboard.** appears. |

---

## Expected Final State

Copy markdown and Copy text icons are available under the user message and each click is confirmed by a toast.

---

## Pass/Fail Criteria

**Pass:**
- **Copy markdown** and **Copy text** icons are visible and clickable.
- After each click a confirmation toast appears.

**Fail:**
- Either icon is missing or not clickable.
- No confirmation toast appears after clicking.

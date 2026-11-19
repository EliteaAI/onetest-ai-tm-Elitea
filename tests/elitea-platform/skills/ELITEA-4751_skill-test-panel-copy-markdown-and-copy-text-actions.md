---
id: ELITEA-4751
title: "Skill test panel: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:chat, feat:skills, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#5838"]
---

# ELITEA-4751: Skill test panel: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Skill test panel: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast.

---

## Preconditions

- User is logged in to {{base_url}} in a project where they can edit entities (e.g. **Bugs & Features**).
- A skill exists (e.g. **potential-bug** with instructions `reply echo`).

---

## Test Data

| Field | Value |
|-------|-------|
| Skill | any existing skill, e.g. potential-bug |
| Message | any text, e.g. `run` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Skills** in the left menu and open the skill | Skill page opens with **Settings** and **Instructions (SKILL.md)**; **Test** button is visible. |
| 2 | Click **Test** | **Test** panel opens on the right with an input box. |
| 3 | Enter the message from Test Data and click the send arrow | Skill output is generated and shown in the Test panel. |
| 4 | Observe the icons below the skill output | **Copy markdown** (M icon) and **Copy text** (copy icon) are visible. |
| 5 | Hover the **M** icon in the skill output toolbar | Tooltip **Copy markdown** is shown. |
| 6 | Click **Copy markdown** | Icon is clickable; confirmation toast **Markdown copied to clipboard.** appears. |
| 7 | Hover the copy icon next to it in the skill output toolbar | Tooltip **Copy text** is shown. |
| 8 | Click **Copy text** | Icon is clickable; confirmation toast **Text copied to clipboard.** appears. |

---

## Expected Final State

Copy markdown and Copy text icons are available under the skill output and each click is confirmed by a toast.

---

## Pass/Fail Criteria

**Pass:**
- **Copy markdown** and **Copy text** icons are visible and clickable.
- After each click a confirmation toast appears.

**Fail:**
- Either icon is missing or not clickable.
- No confirmation toast appears after clicking.

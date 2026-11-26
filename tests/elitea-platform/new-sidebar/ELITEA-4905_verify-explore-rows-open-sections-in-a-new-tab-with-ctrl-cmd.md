---
id: ELITEA-4905
title: "Verify Explore rows open sections in a new tab with Ctrl/Cmd-click and middle-click"
priority: high
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4905: Verify Explore rows open sections in a new tab with Ctrl/Cmd-click and middle-click


## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Click type | Ctrl-click (Windows) / Cmd-click (macOS); Middle-click |
| Sections | Agents; Credentials |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Hover **Explore** | The section list opens |
| 2 | Hover a section row | The browser shows the section's URL in the status bar (it is a real link) |
| 3 | Ctrl/Cmd-click **Agents** (link target `/agents`) | The Agents page opens in a new tab, and the current tab stays on its page |
| 4 | Middle-click **Credentials** | The Credentials page opens in a new tab |
| 5 | Return to the original tab | The page and sidebar state are unchanged |

## Expected Final State

The section pages are open in new tabs, and the original tab is unchanged.

## Pass/Fail Criteria

**Pass:**
- Both click types open the correct section in a new tab

**Fail:**
- The current tab navigates instead, or no new tab opens

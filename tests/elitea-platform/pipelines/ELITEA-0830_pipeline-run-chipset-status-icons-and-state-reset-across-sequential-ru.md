---
id: ELITEA-0830
title: "Pipeline Run Chipset — Status Icons and State Reset Across Sequential Runs"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, story:2186]
requirements: [ProjectAlita/projectalita.github.io#2186]
---
# ELITEA-0830: Pipeline Run Chipset — Status Icons and State Reset Across Sequential Runs

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the run chipset displays the correct, visually distinct status icon for each pipeline run state — and that each new run correctly resets to "In Progress" without inheriting the terminal state from the previous run.

**Coverage (parametrized):**

| Dimension | Values |
|---|---|
| Status icon | In Progress (blue loading) / Completed (green checkmark) / Stopped (orange stop) / Error (red info) |
| Run number | 1st run / 2nd run / 3rd run in same session (no page refresh) |

## Preconditions

- "Valid Pipeline" exists: LLM node (System: "You must create story", Task: "Create some interesting long story"), set as entrypoint, connected to END, saved. Open on Configuration tab → Flow View.
- "Error Pipeline" exists: identical structure but LLM node Task field is empty (triggers execution error). Open on Configuration tab → Flow View.
- All runs executed via chat input in Configuration tab (Flow View) — never via the Run tab.

## Test Data

- Valid Pipeline chat input: "run"
- Error Pipeline LLM node Task field: empty string (triggers error)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Valid Pipeline → Configuration tab → Flow View. Type "run" in the chat input (bottom-right of Configuration page). Press Enter. | Pipeline starts. Run chipset immediately appears with a blue loading/spinner icon and label "Run 1". Icon is animated. |
| 2 | While Run 1 is still In Progress, observe the chipset icon. | Blue loading icon remains visible. Chipset does NOT show "Completed", "Error", or "Stopped" at this stage. |
| 3 | Wait for Run 1 to complete successfully. | Status icon transitions to a green checkmark (green color). "Run 1" label remains. |
| 4 | Without refreshing the page, type "run" again in the chat input. Press Enter to start Run 2. | Chipset immediately shows blue loading icon for Run 2. It does NOT carry over the green checkmark from Run 1 at the start of the new run. |
| 5 | While Run 2 is In Progress, click the Stop button on the chipset. | Run stops. Chipset icon transitions from blue loading to orange stop icon (orange color). "Run 2" label remains. |
| 6 | Without refreshing the page, type "run" in chat input. Press Enter for Run 3. | Chipset immediately shows blue loading icon for Run 3 — NOT orange from Run 2. |
| 7 | Wait for Run 3 to complete successfully. | Icon transitions to green checkmark. No stale state from prior runs. |
| 8 | Open Error Pipeline → Configuration tab → Flow View. Type "run" in chat input. Press Enter. Wait for failure. | Chipset shows blue loading initially, then transitions to red info icon (red color) on failure. |
| 9 | Verify all 4 icon types are visually distinguishable from each other. | Blue ≠ Green ≠ Orange ≠ Red — distinct in both color and icon shape. |

## Expected Final State

Blue ≠ Green ≠ Orange ≠ Red — distinct in both color and icon shape.

## Pass/Fail Criteria

**Pass:**
- Blue loading icon on every run start (including 2nd and 3rd — no state bleed from previous run)
- Green checkmark after successful completion
- Orange stop icon after manual stop
- Red info icon after execution failure
- All icons visually distinct

**Fail:**
- Any run starts showing a terminal state (Completed/Error/Stopped) immediately at launch
- 2nd or 3rd run inherits the previous run's terminal state icon
- Any state shows the wrong icon
- Icons are visually indistinguishable

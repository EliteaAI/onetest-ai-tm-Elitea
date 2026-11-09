---
id: ELITEA-4533
title: "Verify the Raw JSON view on the toolkit Configuration page round-trips correctly and validates JSON syntax inline"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit open in edit mode, with a valid credential selected

## Test Data

| Field | Value |
|-------|-------|
| View toggle | Form view, Raw JSON view |
| Malformed JSON | A duplicate key or unclosed bracket |
| Out-of-bound JSON value | `"max_results": 999` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch from Form view to Raw JSON view | Displayed JSON accurately reflects every Form-view field (name, settings, selected_tools, domains, max_search_depth, per_run_call_cap, credential reference, `"type": "tavily"`) |
| 2 | Inspect the credential reference object in the JSON | Includes `configuration_uuid`, `configuration_project_id`, `private` — never the literal API key value |
| 3 | Introduce a JSON syntax error and observe | An inline "Invalid JSON format" indicator appears; "Save" and "Discard" both become disabled while invalid |
| 4 | Fix the syntax but set `"max_results": 999`, attempt to save | Same server-side validation error as the equivalent Form-view edit (or document any difference) |
| 5 | Switch back to Form view after a valid raw-JSON edit | Form fields reflect the edited values correctly |
| 6 | With a pending invalid-JSON edit, navigate away from the page | A warning/confirmation appears, or the edit is simply not saved — no silent loss or crash |

## Expected Final State

Raw JSON view is confirmed to round-trip accurately and enforce the same validation as Form view.

## Pass/Fail Criteria

**Pass:**
- JSON view matches Form view exactly
- Syntax errors block Save/Discard
- Out-of-bound values are rejected consistently with Form view

**Fail:**
- JSON view diverges from Form view
- A syntax error is not caught
- An out-of-bound JSON value saves successfully

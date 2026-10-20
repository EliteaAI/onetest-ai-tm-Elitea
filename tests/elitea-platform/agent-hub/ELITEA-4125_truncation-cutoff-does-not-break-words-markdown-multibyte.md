---
id: ELITEA-4125
title: "Verify truncation cut-off does not break mid-word, mid-markdown-syntax, or mid-multibyte character"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}` with permissions to create, edit, and publish agents

## Test Data

| Field | Value |
|-------|-------|
| Welcome message | Text containing **bold**, *italic*, and a [link](https://example.com), plus emoji (😀) and accented characters (café, naïve), long enough to exceed the 8-line clamp |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Publish an agent with the welcome message from Test Data | Agent publishes successfully |
| 2 | Open Agents Studio and locate the agent's card | Card is visible |
| 3 | Inspect the clamped/truncated preview text before expanding | No visibly broken Markdown syntax (e.g. lone `**` or incomplete `[text](`) and no garbled/mojibake emoji or accented character at the clamp boundary |
| 4 | Click "Show more" to expand | Full text is displayed |
| 5 | Verify Markdown renders correctly (bold/italic/link applied) and all Unicode/multibyte characters display correctly | All formatting and characters render correctly |

## Expected Final State

Both the clamped preview and the expanded view render Markdown and multibyte characters correctly, with no visual corruption at the truncation boundary.

## Pass/Fail Criteria

**Pass:**
- No broken Markdown syntax or garbled characters are visible in the clamped preview; full, correct rendering appears in the expanded view

**Fail:**
- Clamped preview shows broken Markdown tags or garbled/mojibake characters at the cut-off point
- Expanded view fails to render Markdown or multibyte characters correctly

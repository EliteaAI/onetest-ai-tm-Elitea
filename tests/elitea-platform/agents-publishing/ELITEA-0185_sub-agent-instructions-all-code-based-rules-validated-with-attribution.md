---
id: ELITEA-0185
title: "Sub-Agent Instructions — All Code-Based Rules Validated with Attribution"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [execute_request, feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0185: Sub-Agent Instructions — All Code-Based Rules Validated with Attribution

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify each sub-agent's instructions are checked independently by code-based rules (no LLM) and issues are attributed to the specific sub-agent.

**Coverage:**
- Sub-agent with empty instructions → Critical (attributed)
- Sub-agent with instructions < 100 characters → Critical (attributed)
- Sub-agent with placeholder text (TODO / TBD / Lorem ipsum) → Critical (attributed)
- Valid sub-agent (≥100 chars, no placeholder) → No issue
- Issue attribution format: "Sub-agent '[name]': Instructions [issue]"

## Preconditions

Agent configured with 2 sub-agents:
- DataFetcher: instructions to be set per row
- Summarizer: valid instructions ≥ 100 chars, no placeholder text

## Test Data

| Row | DataFetcher instructions | Expected |
|-----|--------------------------|---------|
| A | (empty) | Critical issues — attributed to DataFetcher |
| B | "Fetch data." (under 100 chars) | Critical issues — attributed to DataFetcher |
| C | "TODO: add instructions" | Critical issues — attributed to DataFetcher |
| D | 100+ chars, valid instructions | Absent from all sections |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set DataFetcher instructions to the value from Row A | DataFetcher instructions updated |
| 2 | Click Publish → enter version name → accept agreement → click Publish | Validation runs; results panel shown |
| 3 | Check Critical issues section for DataFetcher attribution | Critical issue present attributed to DataFetcher (e.g. "Sub-agent 'DataFetcher': Instructions is empty") |
| 4 | Check all sections for any mention of Summarizer | Summarizer absent from Critical, Warnings, and Suggestions |
| 5 | Repeat steps 1–4 for Rows B and C, then Row D | Row B: Critical (too short, <100 chars) for DataFetcher; Row C: Critical (placeholder text) for DataFetcher; Row D: DataFetcher absent from all sections |

## Expected Final State

Row B: Critical (too short, <100 chars) for DataFetcher; Row C: Critical (placeholder text) for DataFetcher; Row D: DataFetcher absent from all sections

## Pass/Fail Criteria

Pass: DataFetcher Critical issues attributed by name for each failing row; Summarizer absent from all sections.
Fail: Issue not attributed to the sub-agent; Summarizer incorrectly flagged; any Critical scenario missing.

---
id: ELITEA-0181
title: "Validation Uses Agent's Configured LLM and Falls Back When Unavailable"
priority: critical
type: functional
module: agents-publishing
status: deprecated
execution_type: manual
tags: [feat:agents, story:4162, story:3774]
requirements: [ProjectAlita/projectalita.github.io#3774, ProjectAlita/projectalita.github.io#4092]
---
# ELITEA-0181: Validation Uses Agent's Configured LLM and Falls Back When Unavailable

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify validation uses the agent's configured LLM and falls back to a system LLM when unavailable.

**Coverage:**
- Agent's LLM used when available
- Falls back to system LLM when agent's LLM is unavailable
- Results still returned after fallback — feature does not break

## Preconditions

- Agent A: valid, available LLM model configured
- Agent B: invalid or unavailable LLM endpoint configured

## Test Data

- Agent A: any agent with valid LLM model
- Agent B: agent configured with an invalid/unavailable LLM endpoint

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A → click Publish → enter version name → accept agreement → click Publish | Validation completes; results panel shown |
| 2 | Open Agent B → click Publish → enter version name → accept agreement → click Publish | Validation starts; LLM failure detected internally; falls back to system LLM |
| 3 | Observe the results panel for Agent B | Results panel shown; no crash or blank screen |

## Expected Final State

Results panel shown; no crash or blank screen

## Pass/Fail Criteria

**Pass:**
- Agent A validation completes successfully
- Agent B validation falls back and still returns a results panel
- No error screen or crash on Agent B

**Fail:**
- Agent B validation fails entirely with no results returned
- Error screen shown instead of results panel
- App crashes or hangs on Agent B

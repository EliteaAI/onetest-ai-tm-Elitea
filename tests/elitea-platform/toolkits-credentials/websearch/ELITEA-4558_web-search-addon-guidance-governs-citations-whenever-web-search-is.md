---
id: ELITEA-4558
title: "WEB_SEARCH_ADDON guidance governs citations whenever Web Search is bound except Swarm Mode"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Web Search is enabled
- Swarm Mode module is available for comparison

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt | A current-events question |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With only Web Search enabled (Swarm Mode off), ask the test prompt | Response cites sources as markdown links; no raw confidential-looking query echoes appear |
| 2 | Enable Swarm Mode alongside Web Search and repeat a similar prompt | Note whether citation/guidance behavior differs from step 1 (documented known gap); response does not crash or appear obviously broken |
| 3 | Review both responses for any "Sources" footer, loading placeholder text, or custom result card UI | None of these elements are rendered in either case; citations appear purely as inline markdown links |

## Expected Final State

Web search guidance (citation format, caution about untrusted content) is consistently applied outside Swarm Mode, with the Swarm Mode gap behaving predictably rather than crashing.

## Pass/Fail Criteria

**Pass:**
- Citations are markdown links in the non-Swarm case; Swarm Mode case does not crash; no Sources footer/loading text/custom cards appear in either case

**Fail:**
- Citations are missing/malformed outside Swarm Mode, the Swarm Mode case crashes, or disallowed UI elements (Sources footer, custom cards) appear

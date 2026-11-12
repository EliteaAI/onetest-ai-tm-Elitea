---
id: ELITEA-4562
title: "Pipelines do not expose a pipeline-level Web Search module toggle"
priority: medium
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Access to an existing pipeline's configuration/canvas view

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline areas to check | Modules section, Advanced settings, Configuration tab, entry-point/trigger settings |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline's configuration/canvas view | View loads |
| 2 | Look for a pipeline-level "Modules" section (as distinct from an individual agent node's own Modules) | No "Web Search" toggle is exposed at the pipeline level |
| 3 | Check pipeline-level Advanced settings, Configuration tab, and entry-point/trigger settings | None of these contain a Web Search option |

## Expected Final State

No pipeline-level Web Search toggle exists anywhere in the pipeline's own configuration surfaces.

## Pass/Fail Criteria

**Pass:**
- No Web Search option appears in any pipeline-level configuration area

**Fail:**
- A Web Search toggle or option appears at the pipeline level itself

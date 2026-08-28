---
id: ELITEA-2932
title: "Pipeline Toolkit node: Skip on a Toolkit node's auth is handled cleanly by the pipeline without corrupting downstream nodes"
priority: high
type: integration
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A pipeline exists with a Toolkit node (delegated toolkit, no token) followed by at least one downstream node consuming the Toolkit node's output

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Toolkit node (auth required) → downstream node consuming its output |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the pipeline | Run pauses at the Toolkit node; popup appears |
| 2 | Click **Skip** on the Toolkit node's popup | Toolkit node's tool call is not executed |
| 3 | Observe how the pipeline handles the branch relying on the skipped node's output | The branch fails cleanly with a clear error (or a defined fallback), rather than proceeding silently with missing/invalid data |
| 4 | Review the pipeline run's final status/log | Run status clearly indicates the skipped node and its downstream impact; no corrupted or partial data is presented as a successful result |

## Expected Final State

Skipping a Toolkit node's authorization does not allow the pipeline to silently proceed with missing/invalid data; the affected branch fails cleanly with a clear error, and the run status/log accurately reflects the skip.

## Pass/Fail Criteria

**Pass:**
- Downstream nodes relying on skipped output either fail clearly or use a defined fallback — never silently proceed with invalid/missing data
- Run status/log clearly reflects the skipped Toolkit node

**Fail:**
- Pipeline silently continues using missing/invalid/default data as if the Toolkit node succeeded
- Run is reported as fully successful despite the skipped, unresolved Toolkit node

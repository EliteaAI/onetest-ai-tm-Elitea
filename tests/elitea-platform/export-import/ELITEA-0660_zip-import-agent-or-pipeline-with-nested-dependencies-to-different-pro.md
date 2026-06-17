---
id: ELITEA-0660
title: "ZIP Import (Agent or Pipeline with Nested Dependencies) to Different Project — Correct Redirect"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, nfr:usability, eng:frontend]
requirements: [ProjectAlita/projectalita.github.io#3668]
---
# ELITEA-0660: ZIP Import (Agent or Pipeline with Nested Dependencies) to Different Project — Correct Redirect

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that importing a ZIP archive (containing an agent or pipeline with nested dependencies) into a different (non-active) project correctly redirects to the root imported entity in the target project and creates all nested entities in that project.

**Coverage:**
- ZIP import flow for agents and pipelines with nested dependencies
- Project selector correctly targets a non-active project during ZIP import
- Post-import redirect navigates to the root entity detail page in the target project
- All nested dependencies (prompts, datasources, tools, etc.) are created under the target project
- Nested entities do NOT appear in the source/active project
- Project context switches correctly to the target project after redirect

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- At least two projects exist with appropriate write access (Project A — active; Project B — target)
- Project A is set as the currently active / open project
- A ZIP export file from an agent that includes nested dependencies (e.g., prompts, datasources) is available
- A ZIP export file from a pipeline that includes nested dependencies is available
- Browser: any modern Chromium-based browser

## Test Data

- **Active project:** Project A
- **Target project:** Project B (different from Project A)
- **Agent ZIP file:** ZIP export of an agent with at least one nested dependency (e.g., `agent-with-deps.zip`) — created via the export-with-dependencies option
- **Pipeline ZIP file:** ZIP export of a pipeline with at least one nested dependency (e.g., `pipeline-with-deps.zip`)
- **Expected redirect URL after agent ZIP import:** `.../app/[project-b-id]/agents/[root-agent-id]`
- **Expected redirect URL after pipeline ZIP import:** `.../app/[project-b-id]/pipelines/[root-pipeline-id]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Prepare a ZIP export file containing an agent with nested dependencies (e.g., prompts, datasources). | ZIP file is ready for upload. |
| 2 | Open Project A as the active project. | Project A is open and shown as the active project. |
| 3 | Navigate to Agents → click Import. | Import wizard opens. |
| 4 | Upload the agent ZIP file. | File accepted; wizard detects nested dependencies and advances to the project selection step. |
| 5 | In the project selector, choose Project B. | Project B is selected as the import target. |
| 6 | Click Import / confirm. | Import runs; nested dependencies are created in Project B. |
| 7 | Wait for import to complete. | Success state is shown with a 'Got it' button. |
| 8 | Click 'Got it'. | Wizard closes. |
| 9 | Observe the page the application navigates to. | App redirects to the root imported agent detail page in Project B. |
| 10 | Check the project indicator and verify that nested dependencies (prompts, datasources, etc.) are visible in Project B. Then navigate to Project A and verify the same nested entities are NOT present there. | Project B is the active context; all nested entities are visible in Project B and absent in Project A. |
| 11 | Repeat steps 1–10 using a ZIP export file from a pipeline with nested dependencies, importing to Project B. | App redirects to the root pipeline detail page in Project B; all nested entities are under Project B and not Project A. |

## Expected Final State

App redirects to the root pipeline detail page in Project B; all nested entities are under Project B and not Project A.

## Pass/Fail Criteria

**Pass:**
- After agent ZIP import to Project B, app redirects to the root agent detail page in Project B
- After pipeline ZIP import to Project B, app redirects to the root pipeline detail page in Project B
- All nested dependencies land in Project B — not in Project A
- Project B is reflected in the project indicator after redirect
- No errors or broken navigation occur

**Fail:**
- App redirects to Project A (the active project) after import completes
- Root entity or nested dependencies appear in Project A instead of Project B
- "Not found" or access error after redirect
- Any nested dependencies are missing from Project B after import
- Any error message or exception is displayed

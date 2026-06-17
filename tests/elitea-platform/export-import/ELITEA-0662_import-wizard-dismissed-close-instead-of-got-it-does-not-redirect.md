---
id: ELITEA-0662
title: "Import Wizard Dismissed (Close Instead of \"Got It\") Does Not Redirect"
priority: low
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, nfr:usability, eng:frontend]
requirements: [ProjectAlita/projectalita.github.io#3668]
---
# ELITEA-0662: Import Wizard Dismissed (Close Instead of "Got It") Does Not Redirect

**Module:** Export Import · **Priority:** Low · **Type:** Functional

**Objective:** Verify that when the import wizard is closed via the X button (instead of clicking "Got it") after a successful cross-project import, the application does NOT redirect the user and keeps the currently active project unchanged.

**Coverage:**
- Import wizard dismissal via X button after successful import completion
- No redirect occurs when the success dialog is closed via X rather than "Got it"
- Active project context remains unchanged (Project A stays active after dismiss)
- No errors or unintended navigation triggered by wizard close action

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- At least two projects exist with appropriate access (Project A — active; Project B — target)
- Project A is set as the currently active / open project
- A valid agent `.md` export file is available for upload
- Browser: any modern Chromium-based browser

## Test Data

- **Active project:** Project A
- **Target project:** Project B (different from Project A)
- **Import file:** valid agent export in `.md` format (e.g., `test-agent-export.md`)
- **Expected state after dismiss:** URL and breadcrumb still reflect Project A; no redirect to Project B

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Prepare a valid agent .md export file. | File is ready for upload. |
| 2 | Open Project A as the active project and note the current URL. | Project A is open; URL reflects Project A context. |
| 3 | Navigate to Agents → click Import. | Import wizard opens. |
| 4 | Upload the agent .md file. | File accepted; wizard advances to the project selection step. |
| 5 | In the project selector, choose Project B (different from Project A). | Project B is selected as the import target. |
| 6 | Click Import / confirm. | Import runs successfully. |
| 7 | Wait for import to complete — verify the success confirmation dialog appears with a 'Got it' button visible. | 'Got it' button is visible on the success dialog. |
| 8 | Instead of clicking 'Got it', click the X (close) button on the wizard dialog. | Wizard closes. |
| 9 | Check the active project shown in the project indicator. | Project A is still shown as the active project — no context switch has occurred. |
| 10 | Check the current URL and breadcrumb. | URL and breadcrumb still reflect Project A; no redirect to Project B has occurred. |
| 11 | Check for error messages or toast notifications. | No errors or warnings are present. |

## Expected Final State

No errors or warnings are present.

## Pass/Fail Criteria

**Pass:**
- After closing the wizard with X, the user remains in Project A
- URL and breadcrumb still reflect Project A
- No redirect to Project B occurs
- No error messages appear

**Fail:**
- App redirects to Project B after wizard close via X
- Active project switches to Project B unexpectedly
- Error message or exception is displayed after closing the wizard

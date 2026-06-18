---
id: ELITEA-1192
title: "Toolkit with missing credential — Pipeline toolkit node shows credential error"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1192: Toolkit with missing credential — Pipeline toolkit node shows credential error

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a Pipeline references a Toolkit node using a private credential the user doesn't own, the Pipeline configuration surface reflects the error with credential name/ID, and execution fails with an informative message.

**Coverage:**
- Pipeline toolkit node shows credential error including name/ID in configuration view
- Pipeline execution fails at the toolkit node with an informative credential error
- Run Details panel shows the credential error traceable to the toolkit node
- No crash or generic timeout on pipeline run

## Preconditions

- Logged in to {{base_url}} as User B
- A shared Pipeline exists with a Toolkit node referencing a credential (e.g., `test_github_credential`) that User B does not own
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Pipeline: shared pipeline with Toolkit node using GitHub toolkit referencing `test_github_credential`
- User B: does not own `test_github_credential`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Pipelines and open the shared Pipeline with the Toolkit node. | Pipeline canvas is displayed. |
| 2 | Click the Toolkit node that uses the GitHub toolkit with the missing credential. | Node configuration panel opens. |
| 3 | Observe the node configuration for any credential error indicator. | An error is shown that includes the credential name/ID (e.g., `test_github_credential`) and indicates the credential is unavailable. |
| 4 | Run the pipeline. | Pipeline execution starts. |
| 5 | Observe the pipeline execution result. Open Run Details. | Execution fails at the Toolkit node. Run Details shows an informative credential error message referencing `test_github_credential` — not a crash, timeout, or unhandled exception. |

## Expected Final State

Execution fails at the Toolkit node. Run Details shows an informative credential error message referencing `test_github_credential` — not a crash, timeout, or unhandled exception.

## Pass/Fail Criteria

**Pass:**
- Toolkit node configuration shows the credential name/ID in an error state
- Pipeline run fails at the Toolkit node with an informative credential error message
- Run Details attributes the failure to the missing credential

**Fail:**
- No error shown in Toolkit node configuration
- Pipeline crashes or times out without an informative credential error
- Run Details shows a generic unhandled exception with no credential reference

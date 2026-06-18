---
id: ELITEA-1190
title: "Agent with broken toolkit — informative credential error in Agent Chat, Pipeline Agent node, and Chat participant"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1190: Agent with broken toolkit — informative credential error in Agent Chat, Pipeline Agent node, and Chat participant

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that attempting to use an Agent that contains a toolkit with a missing/unavailable credential produces a clear, informative error in Agent Chat, Pipeline (Agent node), and Chat with the Agent as a participant — with no silent failure, crash, or opaque error.

**Coverage:**
- Agent Chat: credential error message includes credential title and project reference
- Pipeline Agent node: execution fails at the node with informative credential error in Run Details
- Chat participant: credential error message returned in chat response
- No crashes, hangs, or generic timeouts in any context

## Preconditions

- Logged in to {{base_url}} as User B
- A shared Agent ("broken_agent") exists containing a toolkit whose credential is unavailable to User B
- User B has project access but does not own the credential referenced by the toolkit
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Agent: shared Agent with a GitHub toolkit referencing `test_github_credential` (unavailable to User B)
- Trigger message: "List my GitHub repositories"
- Expected error pattern: `Value error, Configuration with title 'test_github_credential' not found for project_id N or shared in public_project_id M`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Agents and open the broken Agent. Click Start Chat or navigate to the Agent chat panel. Send message: 'List my GitHub repositories'. | Agent chat response contains a clear credential error referencing `test_github_credential` (e.g., 'Configuration with title test_github_credential not found...'). No generic 'something went wrong' or silent timeout. |
| 2 | Navigate to Pipelines. Create or open a Pipeline. Add an Agent node and select the broken Agent. Run the pipeline. | Pipeline execution fails at the Agent node. Run Details shows an informative credential error message referencing `test_github_credential` — not a crash, hang, or unhandled exception. |
| 3 | Navigate to Chat. Start a new conversation. Add the broken Agent as a participant. Send message: 'List my GitHub repositories'. | Chat response contains the credential error message with the credential title and project reference. Conversation does not crash or hang. |

## Expected Final State

Chat response contains the credential error message with the credential title and project reference. Conversation does not crash or hang.

## Pass/Fail Criteria

**Pass:**
- Agent Chat returns a credential error message with the credential name and project reference
- Pipeline Run Details shows the credential error at the Agent node level
- Chat with broken Agent as participant returns the credential error message
- No crashes, silent timeouts, or generic opaque errors in any context

**Fail:**
- Any context returns a generic error with no credential reference
- Any context silently times out or crashes
- Credential error message is absent in any of the three contexts

---
id: ELITEA-2626
title: "Duplicated Chat Retains AI Participant Configuration"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, ai-configuration, P1]
requirements: [3837]
---
# ELITEA-2626: Duplicated Chat Retains AI Participant Configuration

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that AI participants in a duplicated chat retain their required configuration (model, parameters, tools, etc.).

## Preconditions

- User is logged in to {{base_url}}
- Chat exists with configured AI participants (Agent with specific model, Pipeline with parameters)
- AI participants have specific configuration settings

## Test Data

- URL: {{base_url}}
- Agent with specific model (e.g., GPT-4, Claude)
- Pipeline with specific configuration
- Toolkit with credentials/settings

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat with configured AI participants | Chat opens |
| 2 | View Agent participant configuration (model, tools, parameters) | Document Agent configuration |
| 3 | View Pipeline participant configuration | Document Pipeline settings |
| 4 | View Toolkit configuration/credentials status | Document Toolkit setup |
| 5 | Duplicate the chat | Duplicate created |
| 6 | Open duplicated chat and view Agent configuration | Agent retains same model and tool configuration |
| 7 | Verify Pipeline configuration in duplicate | Pipeline settings match original |
| 8 | Verify Toolkit configuration in duplicate | Toolkit configuration preserved |
| 9 | Send a test message to Agent in duplicate | Agent responds using configured model |
| 10 | Test Pipeline execution if applicable | Pipeline executes with correct configuration |

## Expected Final State

- Agent configuration (model, tools, parameters) preserved
- Pipeline settings maintained
- Toolkit credentials/configuration intact
- AI participants functional with original configuration

## Pass/Fail Criteria

**Pass:**
- Agent model and tools match original
- Pipeline configuration preserved
- Toolkit settings intact
- AI participants respond/function correctly
- No configuration reset or loss

**Fail:**
- Agent uses different model than original
- Pipeline configuration lost or reset
- Toolkit credentials missing
- AI participants non-functional
- Configuration requires re-setup

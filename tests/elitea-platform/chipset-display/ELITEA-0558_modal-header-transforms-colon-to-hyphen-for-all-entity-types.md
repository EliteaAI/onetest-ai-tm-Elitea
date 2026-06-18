---
id: ELITEA-0558
title: "Modal Header Transforms Colon to Hyphen for All Entity Types"
priority: high
type: functional
module: chipset-display
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0558: Modal Header Transforms Colon to Hyphen for All Entity Types

**Module:** Chipset Display · **Priority:** High · **Type:** Functional

**Objective:** Verify that when clicking any chipset to open its detail modal, the modal header replaces `:` with ` - `; and that LLM chipset modals show a clean header with no artifacts.

**Coverage:**
- Internal Tool modal header: colon replaced with ` - ` (e.g., "Attachments - createFile")
- Toolkit modal header: colon replaced; user-defined casing preserved (e.g., "myJiraTracker - createIssue")
- MCP modal header: colon replaced; name-embedded hyphen preserved (e.g., "Slack-MCP - sendMessage")
- LLM modal header: no colon to replace; no extra hyphens or artifacts injected (e.g., "GPT-4o Mini")

## Preconditions

- Logged in to ELITEA at {{base_url}}
- An Agent with LLM, Attachments internal tool, Toolkit "myJiraTracker", and MCP "Slack-MCP" configured and run — execution trace is visible
- Browser: Chrome/Edge latest

## Test Data

- Chipset label → expected modal header:
  - "Attachments: createFile" → "Attachments - createFile"
  - "myJiraTracker: createIssue" → "myJiraTracker - createIssue"
  - "Slack-MCP: sendMessage" → "Slack-MCP - sendMessage"
  - "GPT-4o Mini" → "GPT-4o Mini" (no change)
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Run an agent that uses an LLM, an Internal Tool (e.g., Attachments), a Toolkit (e.g., myJiraTracker), and an MCP (e.g., Slack-MCP), so all four chipset types appear in the execution trace. Wait for the run to complete. | Execution trace is visible and contains chipsets for all four entity types. |
| 2 | In the execution trace panel, locate the Internal Tool chipset (e.g., the one labeled 'Attachments: createFile'). | The chipset is identifiable by the Attachments icon and label. |
| 3 | Click on the 'Attachments: createFile' chipset. | A detail modal opens. |
| 4 | Read the modal header text carefully. | Modal header reads 'Attachments - createFile' — the colon (:) from the chipset label has been replaced by a space-hyphen-space ( - ). |
| 5 | Close the modal by clicking the X button or pressing Escape. | Modal closes; execution trace is visible again. |
| 6 | Locate the Toolkit chipset labeled 'myJiraTracker: createIssue'. Click on it. | A detail modal opens. |
| 7 | Read the modal header. | Modal header reads 'myJiraTracker - createIssue' — colon replaced with ' - '; user-defined name casing is preserved. |
| 8 | Close the modal. Locate the MCP chipset labeled 'Slack-MCP: sendMessage'. Click on it. | A detail modal opens. |
| 9 | Read the modal header. Pay attention to the hyphen in 'Slack-MCP' (part of the name) and the separator between name and action. | Modal header reads 'Slack-MCP - sendMessage' — the name hyphen is preserved and the colon separator is replaced with ' - ' (distinct from the name hyphen). |
| 10 | Close the modal. Locate the LLM chipset (e.g., 'GPT-4o Mini'). Click on it. | A detail modal opens. |
| 11 | Read the modal header for the LLM. | Modal header reads 'GPT-4o Mini' — no extra hyphens, dashes, or other formatting artifacts have been injected around the name. |

## Expected Final State

Modal header reads 'GPT-4o Mini' — no extra hyphens, dashes, or other formatting artifacts have been injected around the name.

## Pass/Fail Criteria

**Pass:**
- All modal headers with colons show the colon replaced with " - " (space-hyphen-space)
- LLM modal header shows clean name with no extra hyphens or formatting artifacts
- The embedded hyphen in "Slack-MCP" is preserved and not confused with the separator

**Fail:**
- Any modal header still shows ":" where it should be " - "
- LLM modal header has unexpected extra hyphens or formatting artifacts
- Name-embedded hyphen in MCP name is stripped or doubled

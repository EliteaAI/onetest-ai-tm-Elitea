---
id: ELITEA-1182
title: "Agent and Pipeline Toolkits panel shows all three credential indicators with warning message for invalid credentials; valid credentials show only \"Open in new tab\""
priority: critical
type: functional
module: credential-actions-and-status-indicators
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.toolkits.test_toolkit_indicators_for_credentials.TestAgentCredentialIndicators.test_agent_credential_indicators_e2e
  - tests.ui.toolkits.test_toolkit_indicators_for_credentials.TestPipelineCredentialIndicators.test_pipeline_credential_indicators_e2e
tags: [feat:credentials, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5114]
---
# ELITEA-1182: Agent and Pipeline Toolkits panel shows all three credential indicators with warning message for invalid credentials; valid credentials show only "Open in new tab"

**Module:** Credential Actions And Status Indicators · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Agent menu and the Pipeline configuration Toolkits panel (left side, TOOLS section) expose "Open in new tab", "Reload", Warning/Error status indicator, and a clear warning text message for invalid credentials — each with a correct tooltip — while valid credentials show only the "Open in new tab" icon. For Pipelines, a toolkit is added to the pipeline by adding a Toolkit node and an LLM node on the Flow canvas and selecting the toolkit in each; the warning must also be shown distinctly on the Toolkit node and on the LLM node.

**Coverage:**
- "Open in new tab" icon present and with tooltip in Agent menu (invalid credential)
- "Reload" icon present and with tooltip in Agent menu (invalid credential)
- Warning/Error indicator present in Agent menu (invalid credential)
- Warning text message containing "Authentication failed:" displayed in Agent menu (invalid credential)
- Valid credentials in Agent menu show only "Open in new tab" — no Reload, no error indicator, no warning message
- Pipeline: toolkit is added through a Toolkit node and an LLM node (no direct "add toolkit" to the pipeline)
- Pipeline: "Open in new tab", "Reload", Warning/Error indicator and warning text "Authentication failed:" in the left-side Toolkits panel (invalid credential)
- Pipeline: warning shown separately on the Toolkit node and on the LLM node (invalid credential)
- Pipeline: valid credentials show only "Open in new tab" in the left-side panel — no Reload, no error indicator, no warning — and no warning on the Toolkit node or the LLM node

## Preconditions

- User logged into {{base_url}}
- Agent A configured with a toolkit referencing an invalid credential
- Agent B (or same agent with another toolkit) configured with a toolkit referencing a valid credential
- Pipeline A: a new or existing pipeline with no toolkit nodes yet (toolkits are added during the test through nodes)
- Pipeline B: a new or existing pipeline with no toolkit nodes yet
- A saved toolkit referencing an invalid credential is available in the project (used in Pipeline A)
- A saved toolkit referencing a valid credential is available in the project (used in Pipeline B)

## Test Data

| Field | Value |
|---|---|
| Agent A | agent configured with broken/invalid toolkit credential |
| Agent B | agent configured with correctly authenticated toolkit credential |
| Pipeline A | pipeline without toolkit nodes; the invalid-credential toolkit is added via Toolkit node and LLM node during the test |
| Pipeline B | pipeline without toolkit nodes; the valid-credential toolkit is added via Toolkit node and LLM node during the test |
| Invalid toolkit | saved toolkit referencing a broken/invalid credential |
| Valid toolkit | saved toolkit referencing a correctly authenticated credential |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A (with the invalid credential toolkit) from the Agents section. Navigate to the Agent menu / inline Toolkits panel. | Toolkits panel is visible with credential entries. |
| 2 | Observe the credential entry for the invalid credential. | "Open in new tab" icon is present. |
| 3 | Hover over the "Open in new tab" icon. | Tooltip appears. Text matches expected label (e.g., "Open in new tab"). Not blank. |
| 4 | Observe the same credential entry. | "Reload" icon is present. |
| 5 | Hover over the "Reload" icon. | Tooltip appears. Text matches expected label (e.g., "Reload and apply changes"). Not blank. |
| 6 | Observe the same credential entry. | Warning/Error status indicator is visible. |
| 7 | Observe the text warning message displayed near the credential entry. | Warning message is visible and contains "Authentication failed:" text (e.g., "Authentication failed: Invalid bearer token"). Message is user-friendly, not a raw technical error. |
| 8 | Open Agent B (with the valid credential toolkit). Navigate to the Agent menu / inline Toolkits panel. | Toolkits panel visible with valid credential entry. |
| 9 | Observe the credential entry for the valid credential. | "Open in new tab" icon is visible. |
| 10 | Confirm no Reload icon is shown for the valid credential. | Reload icon is absent for the valid credential entry. |
| 11 | Confirm no Warning/Error status indicator and no warning message is shown for the valid credential. | No error/warning badge and no warning text message displayed for the valid credential. |
| 12 | Open Pipeline A from the Pipelines section and switch to the Flow tab. | Pipeline canvas is displayed. The TOOLS section in the left panel does not list the invalid-credential toolkit yet. |
| 13 | Click "+ Node" and select the **Toolkit** node type. | A Toolkit node is added to the canvas and its configuration panel opens. |
| 14 | In the Toolkit node panel, select the invalid-credential toolkit in the **Toolkit** dropdown and select a tool in the **Tool** dropdown. | Toolkit and tool are selected. The node card shows "<toolkit> › <tool>". |
| 15 | Click "+ Node" and select the **LLM** node type. | An LLM node is added to the canvas and its configuration panel opens. |
| 16 | In the LLM node panel, add the same invalid-credential toolkit to the node's tools (toolkit selector). | The toolkit is attached to the LLM node. |
| 17 | Observe the TOOLS section in the left side of the pipeline page. | The invalid-credential toolkit is listed in the left panel with "Used by" chips for both the Toolkit node and the LLM node. |
| 18 | In the left panel, observe the entry for the invalid-credential toolkit. | "Open in new tab" icon is present. |
| 19 | Hover over the "Open in new tab" icon in the left panel. | Tooltip appears. Text matches expected label (e.g., "Open in new tab"). Not blank. |
| 20 | In the left panel, observe the same entry. | "Reload" icon is present. |
| 21 | Hover over the "Reload" icon in the left panel. | Tooltip appears. Text matches expected label (e.g., "Reload and apply changes"). Not blank. |
| 22 | In the left panel, observe the same entry. | Warning/Error status indicator is visible. |
| 23 | In the left panel, observe the text warning message near the entry. | Warning message is visible and contains "Authentication failed:" text (e.g., "Authentication failed: Invalid bearer token"). Message is user-friendly, not a raw technical error. |
| 24 | Select the **Toolkit node** on the canvas and observe its card/configuration panel. | Warning/Error indicator and the warning message containing "Authentication failed:" are shown for the selected invalid-credential toolkit on the Toolkit node. |
| 25 | Select the **LLM node** on the canvas and observe its card/configuration panel (toolkit selector). | Warning/Error indicator and the warning message containing "Authentication failed:" are shown for the invalid-credential toolkit on the LLM node, independently of the Toolkit node. |
| 26 | Open Pipeline B from the Pipelines section and switch to the Flow tab. | Pipeline canvas is displayed. The TOOLS section in the left panel does not list the valid-credential toolkit yet. |
| 27 | Click "+ Node", select the **Toolkit** node type, then select the valid-credential toolkit and a tool in its configuration panel. | Toolkit node is added and shows "<toolkit> › <tool>". |
| 28 | Click "+ Node", select the **LLM** node type, then add the same valid-credential toolkit to the node's tools. | LLM node is added with the valid toolkit attached. |
| 29 | Observe the TOOLS section in the left side of the pipeline page. | The valid-credential toolkit is listed with "Used by" chips for both nodes. |
| 30 | In the left panel, observe the entry for the valid credential. | "Open in new tab" icon is visible. |
| 31 | Confirm no Reload icon is shown for the valid credential in the left panel. | Reload icon is absent. |
| 32 | Confirm no Warning/Error status indicator and no warning message is shown for the valid credential in the left panel. | No error/warning badge and no warning text message displayed. |
| 33 | Select the **Toolkit node** and then the **LLM node** on the canvas and observe each. | No Warning/Error indicator and no warning message is shown on either the Toolkit node or the LLM node. |

## Expected Final State

No error/warning badge and no warning text message displayed for the valid credential, either in the left-side Toolkits panel or on the Toolkit and LLM nodes of the pipeline.

## Pass/Fail Criteria

**Pass:**
- All three icons/indicators present for invalid credentials in Agent menu
- Tooltips present with meaningful text for "Open in new tab" and "Reload"
- Warning text message containing "Authentication failed:" visible for invalid credentials in Agent menu
- Valid credentials in Agent menu show only "Open in new tab" — no Reload, no warning
- Toolkit can be added to a pipeline via Toolkit node and via LLM node, and is then listed in the left-side TOOLS panel
- All three icons/indicators present for invalid credentials in the Pipeline left-side Toolkits panel
- Tooltips present with meaningful text for "Open in new tab" and "Reload" in the Pipeline left-side panel
- Warning text message containing "Authentication failed:" visible in the Pipeline left-side panel for invalid credentials
- Warning/Error indicator and warning message shown on the Toolkit node and, separately, on the LLM node for invalid credentials
- Valid credentials in Pipeline show only "Open in new tab" in the left-side panel — no Reload, no warning — and no warning on the Toolkit node or LLM node

**Fail:**
- Any icon/indicator missing for invalid credential in Agent menu or in the Pipeline left-side panel
- Any tooltip blank, missing, or showing a raw key
- Warning message absent, does not contain "Authentication failed:", or shows a raw technical error string (e.g., raw JSON/Python traceback)
- Warning missing on the Toolkit node or on the LLM node (shown on only one of them) for an invalid credential
- Reload or Warning/Error indicator shown for a valid credential (left-side panel or on either node)
- "Open in new tab" missing for a valid credential

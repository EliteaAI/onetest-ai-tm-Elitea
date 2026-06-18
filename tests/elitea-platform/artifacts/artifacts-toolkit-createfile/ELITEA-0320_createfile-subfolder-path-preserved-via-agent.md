---
id: ELITEA-0320
title: "createFile Subfolder Path Preserved via Agent"
priority: high
type: functional
module: artifacts-toolkit-createfile
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3690]
---
# ELITEA-0320: createFile Subfolder Path Preserved via Agent

**Module:** Artifacts Toolkit Createfile · **Priority:** High · **Type:** Functional

**Objective:** Verify that `createFile` correctly preserves the subfolder path when invoked through an Agent configured with the Artifact Toolkit.

**Coverage:**
- Agent with Artifact Toolkit (CreateFile enabled)
- User prompt instructs agent to create file at `agentfolder/output.txt`
- File created at correct subfolder path
- Correct path shown in agent tool chipset and Artifacts bucket UI

## Preconditions

- Logged in to next.elitea.ai, Private project
- An Agent in the Private project configured with an Artifact Toolkit having CreateFile enabled
- Artifacts bucket page open in a separate browser tab for visual verification

## Test Data

- Prompt: Create a file at path agentfolder/output.txt with content "agent created this"
- Expected path: agentfolder/output.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Artifacts bucket in a separate browser tab (Artifacts menu → select the bucket). | Bucket file tree is visible and ready for checking. |
| 2 | In the main tab, navigate to Agents → select the Agent configured with the Artifact Toolkit. | Agent chat interface opens. |
| 3 | Send the prompt: 'Create a file at path agentfolder/output.txt with content agent created this'. | Agent processes the request and calls the createFile tool. |
| 4 | Inspect the createFile tool chipset in the chat output. | Chipset shows filename = agentfolder/output.txt; response filepath includes full subfolder path /[bucket]/agentfolder/output.txt — not bare output.txt. |
| 5 | Switch to the Artifacts bucket tab and refresh. | output.txt exists inside agentfolder/. No output.txt at the bucket root. |

## Expected Final State

output.txt exists inside agentfolder/. No output.txt at the bucket root.

## Pass/Fail Criteria

**Pass:**
- Chipset shows correct subfolder path agentfolder/output.txt in both the parameter and response
- File visible at agentfolder/output.txt in Artifacts bucket UI; no file at root

**Fail:**
- Chipset shows bare filename output.txt
- File placed at bucket root instead of agentfolder/

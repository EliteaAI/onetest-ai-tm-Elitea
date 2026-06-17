---
id: ELITEA-0321
title: "createFile Subfolder Path Preserved via Chat with Artifact Toolkit"
priority: high
type: functional
module: artifacts-toolkit-createfile
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3690]
---
# ELITEA-0321: createFile Subfolder Path Preserved via Chat with Artifact Toolkit

**Module:** Artifacts Toolkit Createfile · **Priority:** High · **Type:** Functional

**Objective:** Verify that `createFile` correctly preserves the subfolder path when the Artifact Toolkit is added as a participant in a Chat conversation and the tool is invoked via natural language.

**Coverage:**
- Artifact Toolkit added to Chat as participant
- `createFile` triggered via user prompt with subfolder path in filename
- File created at correct subfolder path `chatfolder/chattest.txt`
- Correct path shown in tool chipset and Artifacts bucket UI

## Preconditions

- Logged in to next.elitea.ai, Private project
- Artifact Toolkit with CreateFile enabled
- Toolkit added as participant in an open Chat conversation
- Artifacts bucket page open in a separate browser tab for visual verification

## Test Data

- Prompt: Create a file named chatfolder/chattest.txt with content "chat created this"
- Expected path: chatfolder/chattest.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Artifacts bucket in a separate browser tab (Artifacts menu → select the bucket). | Bucket file tree is visible and ready for checking. |
| 2 | In the main tab, open a Chat conversation with the Artifact Toolkit added as a participant. | Toolkit appears in the Participants panel. |
| 3 | Send the prompt: 'Create a file named chatfolder/chattest.txt with content chat created this'. | LLM invokes the createFile tool. |
| 4 | Inspect the tool chipset output in the chat. | Chipset shows filename = chatfolder/chattest.txt was passed to the tool; response shows full subfolder path /[bucket]/chatfolder/chattest.txt — not bare chattest.txt. |
| 5 | Switch to the Artifacts bucket tab and refresh. | chattest.txt exists inside chatfolder/. No chattest.txt at the bucket root. |

## Expected Final State

chattest.txt exists inside chatfolder/. No chattest.txt at the bucket root.

## Pass/Fail Criteria

**Pass:**
- Tool chipset shows correct subfolder path chatfolder/chattest.txt in both the parameter and response
- File visible at chatfolder/chattest.txt in Artifacts bucket UI; no file at root

**Fail:**
- Chipset shows bare filename chattest.txt
- File placed at bucket root instead of chatfolder/

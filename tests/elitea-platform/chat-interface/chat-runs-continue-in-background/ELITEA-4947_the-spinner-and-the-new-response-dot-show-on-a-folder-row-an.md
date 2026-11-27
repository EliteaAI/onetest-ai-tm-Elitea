---
id: ELITEA-4947
title: "The spinner and the New response dot show on a folder row and a pinned row"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:social-folders, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Run indicators appear on chats inside folders and on pinned chats, not only on ungrouped rows.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **AF** in a chat folder and conversation **AP** pinned, both with R7385LongRunner as the participant
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Messages | `The word is M05F.` in AF, `The word is M05P.` in AP |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send in AF, then open B | AF's row in the folder shows the spinner with "Generating…" |
| 2 | After AF ends | AF's row shows the "New response" dot |
| 3 | Open AF | The dot clears |
| 4 | Repeat for the pinned chat AP | The same spinner, dot, and clearing on the pinned row |

## Expected Final State

Both rows showed and cleared the indicators.

## Pass/Fail Criteria

**Pass:**
- Spinner and dot appear on both rows and clear on open

**Fail:**
- A folder or pinned row shows no spinner or no dot

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations AF, AP and B, the agent R7385LongRunner and the toolkits `r7385_echo` and `r7385_jph`, then AF's folder.

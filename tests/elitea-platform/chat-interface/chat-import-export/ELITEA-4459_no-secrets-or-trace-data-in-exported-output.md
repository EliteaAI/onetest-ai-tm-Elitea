---
id: ELITEA-4459
title: "Export (and the reconstructed data Import reads from it) never contains secrets or internal trace data"
priority: critical
type: security
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, security, issue:6903, p0]
requirements: ["EliteaAI/elitea_issues#6903"]
---

# ELITEA-4459: Export (and the reconstructed data Import reads from it) never contains secrets or internal trace data

**Module:** chat-interface · **Priority:** Critical · **Type:** Security

**Objective:** Confirm that exported chat data (and the data Import reconstructs from it) never contains API keys, tokens, credentials, raw tool-call JSON payloads, or internal reasoning/trace steps.

---

## Preconditions

- A toolkit available in the project that can be invoked from chat (e.g. a file-listing toolkit).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a chat. Send a first message that invokes the toolkit (e.g. ask it to list files via the toolkit). | AI responds using the toolkit; response is added to the chat. |
| 2 | Export this chat "With attachments". Inspect the resulting data — directly if this environment's exports are unencrypted, or via Import's reconstructed conversation record (DevTools network response after importing into any project) if exports are encrypted. | No API keys, tokens, credentials, raw tool-call JSON payloads, or internal reasoning/trace steps appear anywhere in the exported/reconstructed data — only plain message text, attachment references, and basic LLM settings (e.g. model name, no key). |

## Expected Final State

No sensitive data or internal trace data appears anywhere in the export output.

## Pass/Fail Criteria

**Pass:**
- No secrets, credentials, or trace data found.

**Fail:**
- Any secret/credential/trace data found.

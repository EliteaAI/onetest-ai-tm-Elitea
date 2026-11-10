---
id: ELITEA-4456
title: "Export menu placement/visibility rules and the modal's exact text in every attachment state"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, issue:6903, p1]
requirements: ["EliteaAI/elitea_issues#6903"]
---

# ELITEA-4456: Export menu placement/visibility rules and the modal's exact text in every attachment state

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the `Export` action appears directly after `Duplicate` in the chat `...` menu, is hidden for Playback chats, is disabled while the canvas is being edited, and that the Export modal shows the exact specified text for its no-attachments, zero-attachments-disabled, and with-attachments states, with all three cancel paths working cleanly.

---

## Preconditions

- A project/environment with chat creation available.
- A Playback chat (`[Playback] ...`), if available in the test environment (skip the Playback step if none exists).

## Test Data

| Field | Value |
|-------|-------|
| First message (chat 1) | "Hello, make use this chat?" |
| First message (chat 2) | "Create sample csv file artifact" (agent/tool generates 1 file into Artifacts) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new chat. Send the first message "Hello, make use this chat?". Do not attach any file. | New chat is created, auto-named "Hello, make use this chat?" from the first message. |
| 2 | Open the `...` menu on this chat. | `Export` appears directly after `Duplicate`, with a download icon matching the other menu items' style. |
| 3 | Open the `...` menu on a Playback chat (if available). | `Export` is not shown at all (hidden, not disabled). |
| 4 | On the non-Playback chat, start editing its canvas (if a canvas exists or can be created), then open the `...` menu. | `Export` is visible but disabled. |
| 5 | On the "Hello, make use this chat?" chat (zero attachments), click Export. | Modal shows exactly: "Export chat" / "Hello, make use this chat?" / "Without attachments" (selected) / "With attachments" / "Only chat messages will be exported as a JSON file." / Cancel and Export buttons. "With attachments" is disabled; hovering it shows tooltip "This chat has no attachments." |
| 6 | Create a second chat. Send the first message "Create sample csv file artifact", and have an agent/tool generate one file into the Artifacts bucket as part of the response (so the chat ends up with exactly 1 available attachment). Click Export. | Modal shows: "Export chat" / "Create sample csv file artifact" / "Without attachments" (selected) / "With attachments (1 file)" / "Only chat messages will be exported as a JSON file." / Cancel and Export. |
| 7 | On this modal, select the "With attachments" radio. | The description line changes to: "Chat messages and all attached and generated files/images will be exported as a ZIP archive." / "The archive will be downloaded by your browser. Track its progress in the browser downloads." Toggle back to "Without attachments" and confirm the description switches back correctly. |
| 8 | Press Esc without exporting. | Modal closes, nothing downloads. |
| 9 | Reopen, click the X (close) button without exporting. | Modal closes, nothing downloads. |
| 10 | Reopen, click Cancel without exporting. | Modal closes, nothing downloads. |
| 11 | Click Export, then immediately click Export again before it finishes. | Button shows a loading state; the second click has no effect (no duplicate download/request). |

## Expected Final State

Export's menu placement/visibility is correct in every chat state, and the modal's text content is exactly as specified for each selection state.

## Pass/Fail Criteria

**Pass:**
- All quoted text matches exactly; menu visibility/disable rules hold; all 3 cancel paths are clean.

**Fail:**
- Any wording mismatch, wrong menu visibility, or a cancel path that doesn't close cleanly / leaves a download behind.

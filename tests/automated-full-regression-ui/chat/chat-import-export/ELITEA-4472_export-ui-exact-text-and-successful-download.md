---
id: ELITEA-4472
title: "Export menu/modal show exact specified text and successfully produce a downloadable export"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, regression, issue:6903, p0]
requirements: ["EliteaAI/elitea_issues#6903"]
---

# ELITEA-4472: Export menu/modal show exact specified text and successfully produce a downloadable export

**Module:** chat-interface · **Priority:** Critical · **Type:** Regression

**Objective:** Confirm Export's entry point, exact modal text, and basic download capability all continue to work correctly.

---

## Preconditions

- Create a chat. Send a first message that results in at least 1 attachment being present (uploaded or generated).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `...` menu on the chat. | `Export` visible, positioned directly after `Duplicate`. |
| 2 | Click Export, "Without attachments" selected (default). | Modal shows exactly: "Export chat" / <chat's auto-derived name> / "Without attachments" / "With attachments (<N> files)" / "Only chat messages will be exported as a JSON file." Export it — JSON downloads successfully. |
| 3 | Export again, "With attachments" selected. | Description switches to "Chat messages and all attached and generated files/images will be exported as a ZIP archive." / "The archive will be downloaded by your browser. Track its progress in the browser downloads." ZIP downloads successfully, containing the attachment(s). |

## Expected Final State

Export's entry point, exact modal text, and basic download capability work correctly.

## Pass/Fail Criteria

**Pass:**
- Exact text matches; both exports download successfully.

**Fail:**
- Export missing/misplaced, wrong modal text, or any download failing/corrupted.

---
id: ELITEA-2620
title: "Chat – Rapid Double-Stop / Stop-Then-Immediately-Resend Edge Case"
priority: low
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2620: Chat – Rapid Double-Stop / Stop-Then-Immediately-Resend Edge Case

**Module:** chat-interface · **Priority:** Low (edge case) · **Type:** Functional

**Objective:** Verify that clicking Stop twice in rapid succession, or clicking Send again the instant text is restored to the input, does not cause duplicate stop calls, crashes, or duplicate/garbled messages.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | "quick stop test" |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send the message and, during the thinking phase, click Stop twice in quick succession (double-click) | No crash or error occurs; only one stop is effectively processed |
| 2 | Verify the input is restored with the exact original text exactly once (not duplicated/concatenated) | Input shows the single, correct original message |
| 3 | Immediately click Send again as soon as the text is restored | Message is sent normally |
| 4 | Verify only one new user message appears (no duplicate sends) | Single message sent; response generation proceeds normally |

---

## Expected Final State

Rapid repeated stop clicks and an immediate resend behave gracefully with no duplication or crashes.

---

## Pass/Fail Criteria

**Pass:**
- No crash, console error, or duplicate stop network calls causing visible issues.
- Input text is restored exactly once, uncorrupted.
- Resend produces exactly one new message.

**Fail:**
- UI crashes or freezes.
- Restored text is duplicated/garbled.
- Resend produces duplicate messages or fails.

---
id: ELITEA-3564
title: "Mentions and HTML Content Are Rendered Correctly in Sent Messages"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3564: Mentions and HTML Content Are Rendered Correctly in Sent Messages

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify `mentions` and `html` parameters behave correctly on both `send_chat_message` and `send_channel_message`.

## Preconditions

- Teams toolkit with `send_chat_message` and `send_channel_message` enabled, linked to an authorized credential
- A valid chat and a valid channel; a second test user's email for mentions

## Test Data

| Variant | Tool | mentions | html | Content |
|---|---|---|---|---|
| A | send_chat_message | recipient's email | false | plain text with mention |
| B | send_channel_message | — | true | simple HTML (bold text, line break) |
| C | send_chat_message | — | false | plain text, no mentions |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a chat message per Variant A | The mention renders as a proper @mention in Teams; the rest of the message text is not corrupted by HTML escaping |
| 2 | Send a channel message per Variant B | Message renders with the formatting applied (bold, line break) in Teams, not as literal tags |
| 3 | Send a chat message per Variant C | Message is delivered as plain text, unmodified |

## Expected Final State

All three sent messages display in Microsoft Teams exactly as intended by their `html`/`mentions` parameters.

## Pass/Fail Criteria

**Pass:**
- Mention resolves to a real @mention; HTML renders formatted; plain text is delivered unmodified

**Fail:**
- Mention appears as raw text/broken link, HTML tags render literally, or plain text is altered/escaped incorrectly

---
id: ELITEA-0639
title: "Messages containing HTML and script-like content are displayed as plain text and not executed"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [input-sanitization, xss-prevention, security, R-2.0.3]
requirements: [#4775, #4773]
---
# ELITEA-0639: Messages containing HTML and script-like content are displayed as plain text and not executed

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** A user may type content that looks like HTML tags or JavaScript. The application must display all user input as literal text only — never rendering or executing it. An XSS vulnerability in a chat widget is exploitable and a critical security finding.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open

## Test Data

- Input 1: <script>alert('XSS')</script>
- Input 2: <b>bold</b> <img src=x onerror=alert(1)>
- Input 3: Hello <World> & "Test" with emoji 🎉

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type <script>alert('XSS')</script> into the message input and send it. | No JavaScript alert dialog appears. The text is shown in the chat bubble exactly as typed, as literal characters. |
| 2 | Type <b>bold</b> <img src=x onerror=alert(1)> into the input and send it. | No alert dialog appears. No bold rendering or image loading occurs. The raw HTML string is shown as plain text in the bubble. |
| 3 | Type Hello <World> & "Test" with emoji 🎉 and send it. | All characters including angle brackets, ampersand, quotes, and emoji render correctly as visible text. |
| 4 | Open the browser developer tools and check the Console tab after all three sends. | No unexpected JavaScript errors, no alert calls, and no unauthorized network requests are visible in the console. |

## Expected Final State

No unexpected JavaScript errors, no alert calls, and no unauthorized network requests are visible in the console.

## Pass/Fail Criteria

Pass:
- No JavaScript alert fires for any of the three inputs
- All inputs displayed as literal text in the chat bubbles
- No HTML tags rendered (no bold, no images loaded)
- No unexpected console errors

Fail:
- A JavaScript alert dialog appears for input 1 or 2
- HTML tags are rendered (text appears bold, an image loads)
- Browser console shows unauthorized script execution

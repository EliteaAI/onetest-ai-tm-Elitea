---
id: ELITEA-3524
title: "send_mail — Send a New Message and Capture Thread Identifiers"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3524: send_mail — Send a New Message and Capture Thread Identifiers

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `send_mail` delivers a message to a real recipient and that the sent message is retrievable afterward with a valid thread/conversation identifier.

## Preconditions

- A disposable secondary mailbox to act as recipient
- Toolkit with `send_mail` enabled, linked to an authorized credential

## Test Data

- To: disposable secondary mailbox address
- Subject: `Outlook Toolkit Test — send_mail {{timestamp}}`
- Body: `This is an automated test message.`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `send_mail` with the test recipient, subject, and body | Call succeeds without error |
| 2 | Check the secondary mailbox's Inbox | The message arrives with matching subject/body |
| 3 | Use `list_messages` on the Sent Items folder of the sender mailbox | The sent message appears with a valid `conversationId`/thread identifier |

## Expected Final State

The email is delivered to the recipient and appears in Sent Items with a valid thread identifier.

## Pass/Fail Criteria

**Pass:**
- Recipient receives the exact subject/body
- Sent message is present in Sent Items with a valid thread identifier

**Fail:**
- Message is not delivered, or delivered with incorrect content
- Sent message is missing from Sent Items or lacks a thread identifier

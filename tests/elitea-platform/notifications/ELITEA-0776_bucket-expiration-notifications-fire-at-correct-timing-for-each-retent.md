---
id: ELITEA-0776
title: "Bucket Expiration Notifications Fire at Correct Timing for Each Retention Type [Parametrized]"
priority: critical
type: functional
module: notifications
status: deprecated
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0776: Bucket Expiration Notifications Fire at Correct Timing for Each Retention Type [Parametrized]

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that bucket expiration notifications are triggered at the correct scheduled intervals for all four retention types (Days, Weeks, Months, Years), and that each notification contains the required content elements.

**Coverage:**
- Days retention: immediate notification on creation — correct expiration date and "in N days" text
- Weeks retention: notification at 5 days before expiration — correct date and "in 5 days" text
- Months retention: two notifications — at 7 days and 1 day before expiration
- Years retention: three notifications — at 30 days, 7 days, and 1 day before expiration
- Each notification contains: ⚠️ icon, clickable bucket name (hyperlink), expiration date + time, time remaining text, action suggestion text

## Preconditions

- Logged in to {{base_url}} as a project member with `artifacts.buckets.create` permission
- Test environment supports date-offset simulation for Weeks/Months/Years threshold testing
- Browser: Chrome (latest)

## Test Data

| Bucket Name | Retention Type | Value | Notification Trigger | Creation Date | Expected Expiry | Expected Remaining Text |
|---|---|---|---|---|---|---|
| `param-days-3` | Days | 3 | Immediate on creation | March 30, 2026 | April 2, 2026 | "in 3 days" |
| `param-weeks-2` | Weeks | 2 | 5 days before expiry | March 2, 2026 | March 16, 2026 | "in 5 days" |
| `param-months-3` | Months | 3 | 7 days before expiry | December 30, 2025 | March 30, 2026 | "in 7 days" |
| `param-months-3` | Months | 3 | 1 day before expiry | December 30, 2025 | March 30, 2026 | "in 1 day" |
| `param-years-1` | Years | 1 | 30 days before expiry | March 30, 2025 | March 30, 2026 | "in 30 days" |
| `param-years-1` | Years | 1 | 7 days before expiry | March 30, 2025 | March 30, 2026 | "in 7 days" |
| `param-years-1` | Years | 1 | 1 day before expiry | March 30, 2025 | March 30, 2026 | "in 1 day" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Click '+ Create Bucket'. Enter name: `param-days-3`, Period Type: Days, Value: 3. Click Save. | Bucket `param-days-3` is created and appears in the sidebar with no error. |
| 2 | Without reloading the page, click the bell icon in the top navigation bar to open the Notification Center. | Notification Center opens. A notification for `param-days-3` is visible immediately. |
| 3 | Verify the notification contains: ⚠️ icon, `param-days-3` as a clickable (underlined) link, expiration date April 2, 2026, text 'in 3 days', and an action suggestion (e.g. 'Consider extending retention or backing up important files'). | All five content elements are present and accurate. |
| 4 | Using date simulation, advance the environment date to March 11, 2026 (5 days before `param-weeks-2` expiry on March 16, 2026). Open the Notification Center. | A notification for `param-weeks-2` appears with expiry date March 16, 2026 and text 'in 5 days'. |
| 5 | Verify all required notification elements for `param-weeks-2`: ⚠️ icon, clickable bucket name, expiration date March 16, 2026, 'in 5 days', action suggestion. | All five elements present and correct. |
| 6 | Using date simulation, advance to March 23, 2026 (7 days before `param-months-3` expiry on March 30, 2026). Open the Notification Center. | A notification for `param-months-3` appears with expiry March 30, 2026 and text 'in 7 days'. |
| 7 | Using date simulation, advance to March 29, 2026 (1 day before `param-months-3` expiry). Open the Notification Center. | A second distinct notification for `param-months-3` appears with text 'in 1 day'. Both the '7 days' and '1 day' entries coexist. |
| 8 | Using date simulation, advance to February 28, 2026 (30 days before `param-years-1` expiry on March 30, 2026). Open the Notification Center. | A notification for `param-years-1` appears with expiry March 30, 2026 and text 'in 30 days'. |
| 9 | Using date simulation, advance to March 23, 2026 (7 days before `param-years-1` expiry). Open the Notification Center. | A second distinct notification for `param-years-1` appears with text 'in 7 days'. |
| 10 | Using date simulation, advance to March 29, 2026 (1 day before `param-years-1` expiry). Open the Notification Center. | A third distinct notification for `param-years-1` appears with text 'in 1 day'. All three entries ('in 30 days', 'in 7 days', 'in 1 day') are independently visible. |

## Expected Final State

A third distinct notification for `param-years-1` appears with text 'in 1 day'. All three entries ('in 30 days', 'in 7 days', 'in 1 day') are independently visible.

## Pass/Fail Criteria

**Pass:**
- All retention types generate notifications at their documented thresholds
- Days: immediate; Weeks: 5 days before; Months: 7 days and 1 day before; Years: 30 days, 7 days, and 1 day before
- Each notification contains all five required elements: ⚠️ icon, clickable bucket name, expiration date, time remaining, action suggestion
- Expiration dates and remaining text are accurate for all scenarios

**Fail:**
- Any scheduled notification is missing or fires at the wrong time
- Any notification is missing a required content element
- Expiration date or time remaining text is inaccurate

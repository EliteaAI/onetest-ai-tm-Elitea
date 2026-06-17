---
id: ELITEA-0990
title: "Secret Creation Input Field Is Immediately Visible When Clicking '+' From Page 2 of Secrets List"
priority: high
type: functional
module: secrets
status: ready
execution_type: manual
tags: [feat:credentials, nfr:usability, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4860]
---
# ELITEA-0990: Secret Creation Input Field Is Immediately Visible When Clicking '+' From Page 2 of Secrets List

**Module:** Secrets · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the "+" (Create a Secret) button while on page 2 (or any non-first page) of the Secrets list makes the new secret creation input field immediately visible to the user — either by appearing on the current page or by auto-navigating to page 1 where the field is rendered.

**Bug Reference:** #4860 — The creation input field is rendered on page 1 while the user remains on page 2, making it invisible and leaving the user unaware that any action occurred.

## Preconditions

- The Secrets page contains enough secrets to span at least 2 pages (pagination is visible)
- User is on page 2 of the Secrets list

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Secrets page and paginate to page 2 of the secrets list | Page 2 of the secrets list is displayed |
| 2 | Click the '+' (Create a Secret) button | The new secret creation input field appears immediately and is visible to the user — either on the current page (page 2) or the user is automatically redirected to page 1 where the input is rendered |
| 3 | Verify the input field is visible without any manual navigation | Input field is visible and ready to accept a secret name without the user needing to manually switch pages |
| 4 | Type a secret name in the input field and save it | Secret is created successfully and appears in the list |

## Expected Final State

Secret is created successfully and appears in the list

## Pass/Fail Criteria

**Pass:**
- The new secret creation input field is immediately visible after clicking "+"
- User does not need to manually navigate to find the input

**Fail:**
- The input field is rendered on page 1 while the user remains on page 2 (invisible)
- No visible feedback is given after clicking "+" — user is unaware of the action

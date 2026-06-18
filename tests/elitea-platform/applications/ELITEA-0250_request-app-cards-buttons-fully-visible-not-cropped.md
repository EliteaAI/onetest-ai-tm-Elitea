---
id: ELITEA-0250
title: "Request App Cards: Buttons Fully Visible — Not Cropped"
priority: medium
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, eng:design, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770, EliteaAI/elitea_issues#4898]
---
# ELITEA-0250: Request App Cards: Buttons Fully Visible — Not Cropped

**Module:** Applications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that "+ Create App" and "> View Configured" buttons on both Request App cards are fully visible with no bottom cropping.

**Coverage:**
- Button borders fully visible on DeepWiki card
- Button borders fully visible on Inventory card
- No bottom clipping on either card

## Preconditions

- Logged in as a project member
- On the Request App tab

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Request App tab | DeepWiki and Inventory cards are displayed |
| 2 | Observe the '+ Create App' button on the DeepWiki card | Button is fully visible with complete border and proper spacing; no cropping at the bottom |
| 3 | Observe the '> View Configured' button on the DeepWiki card | Button is fully visible; no cropping |
| 4 | Observe both buttons on the Inventory card | Both '+ Create App' and '> View Configured' buttons are fully visible on the Inventory card with no cropping |

## Expected Final State

Both '+ Create App' and '> View Configured' buttons are fully visible on the Inventory card with no cropping

## Pass/Fail Criteria

**Pass:**
- All four buttons fully visible with no cropping or clipped borders

**Fail:**
- Any button border clipped or partially hidden at the bottom of the card

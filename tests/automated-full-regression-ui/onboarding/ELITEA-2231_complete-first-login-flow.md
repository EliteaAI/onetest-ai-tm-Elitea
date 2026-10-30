---
id: ELITEA-2231
title: "Onboarding — Complete First Login Flow"
priority: critical
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2231: Onboarding — Complete First Login Flow

**Module:** onboarding · **Priority:** critical · **Type:** functional

**Objective:** Verify the complete first-time user onboarding flow from initial welcome page through project provisioning to successful workspace entry.

---

## Preconditions

- User is logged in to the Elitea platform for the first time with a new user account.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to the application for the first time with a new user account | User is authenticated and lands on the expected landing page. |
| 2 | Verify a full-screen welcome page is displayed with the ELITEA logo at the top center | Condition holds as described. |
| 3 | Verify the page title reads "Welcome to Elitea!" | Condition holds as described. |
| 4 | Verify a card is displayed in the center of the page with the greeting "Hello, [Username]!" (e.g., "Hello, Mariam Test!") | Condition holds as described. |
| 5 | Verify the card body text reads: "We're setting up your personal workspace — it'll be ready in about 5 minutes. While we work our magic, take a quick tour through our onboarding slides!" | Condition holds as described. |
| 6 | Verify the secondary text reads: "Ready to explore Elitea's smart tools and tips?" | Condition holds as described. |
| 7 | Verify a "Sure, let's go!" button is displayed inside the card | Condition holds as described. |
| 8 | Verify no sidebar navigation is visible at this stage (no left panel, no project dropdown) | Condition holds as described. |
| 9 | Verify the Personal/Private project has NOT yet started loading at this point — project provisioning does not begin until the user clicks "Sure, let's go!" | Condition holds as described. |
| 10 | Click the "Sure, let's go!" button | Button click triggers the expected transition. |
| 11 | Verify the welcome card is replaced by the onboarding tips slide view | Condition holds as described. |
| 12 | Verify the ELITEA logo is shown at the top center of the page | Condition holds as described. |
| 13 | Verify the first slide shows "Tip 1: Welcome to ELITEA" as the title | Condition holds as described. |
| 14 | Verify the slide description reads: "ELITEA is your AI-powered workspace where you create intelligent agents, automate workflows with pipelines, and chat with powerful AI models. Everything you need is organized in the left sidebar for easy access." | Condition holds as described. |
| 15 | Verify the Quick Action text reads: "Click the ELITEA logo (top-left) to explore all available menus." | Condition holds as described. |
| 16 | Verify the slide counter shows "1 / 48" | Condition holds as described. |
| 17 | Verify a progress bar is visible at the bottom of the page with the label "Configuring Personal project..." and estimated time "about 5 min" | Condition holds as described. |
| 18 | Verify the Personal/Private project provisioning begins only now — after clicking "Sure, let's go!" — and was not running before | Condition holds as described. |
| 19 | Verify no sidebar navigation is visible yet and no project dropdown is available while the project is still being provisioned | Condition holds as described. |
| 20 | Wait approximately 5 minutes for project provisioning to complete | Wait completes; subsequent state is ready. |
| 21 | Verify the "Your Elitea workspace is ready!" banner with "Jump in now!" button is visible below the onboarding tips card | Condition holds as described. |
| 22 | Verify the Private project appears in the left menu dropdown with a checkmark indicator | Condition holds as described. |
| 23 | Verify team projects (if applicable for the user's account) are now listed in the dropdown | Condition holds as described. |
| 24 | Verify the full sidebar navigation items are now visible: Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, Artifacts, Settings, Catalog | Condition holds as described. |
| 25 | Verify the "Jump in now!" button is visible and styled with a teal/green color | Condition holds as described. |
| 26 | Click the "Jump in now!" button | Control responds; expected next state is shown. |
| 27 | Verify the onboarding card is dismissed/closed | Condition holds as described. |
| 28 | Verify the user is navigated to the default project page (e.g., Chats page) | Condition holds as described. |
| 29 | Verify the full sidebar navigation is displayed and functional | Condition holds as described. |
| 30 | Verify the onboarding card is no longer shown on the screen | Condition holds as described. |

---

## Expected Final State

The onboarding flow is complete: the user has successfully entered their workspace with the onboarding card closed, the sidebar fully displayed with all navigation items (Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, Artifacts, Settings, Catalog), and the Private project loaded in the project dropdown.

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified: Welcome page displayed correctly, "Sure let's go" button clicked, project provisioning started, onboarding tips card shown with progress bar, projects appeared in dropdown after ~5 minutes, "Jump in now!" button clicked, onboarding closed successfully.

**Fail:**
- Any assertion fails, any step produces an error, or any expected UI state is not observed.

---

## Notes

**Source functional tests:** ELITEA-2231, ELITEA-2232, ELITEA-2235, ELITEA-2240, ELITEA-2241

**Regression rationale:** Consolidated from 5 tests to verify the complete first-time login and onboarding flow as a single critical user journey. This ensures all key milestones (welcome page, project provisioning trigger, onboarding display, workspace readiness, and entry) are validated together.

**Selected checkpoints:** Welcome page content and structure, project provisioning timing (does not start until "Sure, let's go!" clicked), onboarding tips card display with slide 1/48, progress bar with "about 5 min" estimate, workspace ready banner, projects appearance in dropdown, sidebar items visibility, successful onboarding dismissal.

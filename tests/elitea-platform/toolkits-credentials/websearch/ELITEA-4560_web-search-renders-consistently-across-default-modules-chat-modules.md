---
id: ELITEA-4560
title: "Web Search renders consistently across Default Modules Chat Modules and Agent Modules"
priority: medium
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Project-admin access to Settings → General

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |
| Expected description text | "Allow the LLM to search the Internet, read web pages, and cite its sources." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → General → Default Modules | "Web Search" row shows title "Web Search," the expected description text, and is positioned sensibly in the module list (between Image Creation and Data Analysis) |
| 2 | Open the Chat Modules flyout | Same label and iconography (globe icon) as Default Modules |
| 3 | Open an Agent's Modules section ("Show all") | Same label, tooltip text, and iconography |
| 4 | Trigger a web search in chat and observe the tool-use chip | Chip uses the existing chip/spinner styling with the label "Web Search," matching other internal tool chips |

## Expected Final State

Web Search is visually and textually consistent across all three surfaces and the chat tool-use indicator.

## Pass/Fail Criteria

**Pass:**
- Label, description, icon, and tooltip match across all locations

**Fail:**
- Any location shows a different label, missing description, wrong icon, or mismatched chip styling

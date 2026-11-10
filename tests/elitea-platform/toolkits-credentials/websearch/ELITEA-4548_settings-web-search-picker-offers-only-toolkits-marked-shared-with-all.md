---
id: ELITEA-4548
title: "Settings → Web Search picker offers only toolkits marked Shared with all projects"
priority: critical
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- User is logged in to `{{base_url}}` as a public-project admin
- At least one Tavily toolkit in the public project is marked "Shared with all projects"

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` (public project) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Tavily toolkit currently used by Settings → Web Search | Toolkit configuration opens |
| 2 | Check the "Shared with all projects" switch state | Switch is ON |
| 3 | Open Settings → General → Web Search in the public project | Web Search section with a toolkit picker is displayed |
| 4 | Review the picker's list of selectable toolkits | List contains only toolkits marked "Shared with all projects"; no non-shared toolkit appears as an option |
| 5 | Compare the currently selected toolkit in the picker to the toolkit observed in step 1 | They match |

## Expected Final State

No state is changed; the picker is confirmed to list only properly shared toolkits.

## Pass/Fail Criteria

**Pass:**
- Only shared toolkits appear in the picker, and the selected toolkit matches the one confirmed shared

**Fail:**
- A non-shared toolkit appears as selectable, or the selected toolkit's shared switch is OFF

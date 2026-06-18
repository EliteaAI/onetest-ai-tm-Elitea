---
id: ELITEA-0177
title: "Admin Can Upload and Publish an Agent From Public Project Admin Section Without AI Validation"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3773, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3773]
---
# ELITEA-0177: Admin Can Upload and Publish an Agent From Public Project Admin Section Without AI Validation

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a platform admin can navigate to the Public Project → Agents Menu → Admin section and manually upload/publish an agent directly to Agents Studio, with AI quality validation bypassed entirely.

**Coverage:**
- Admin section accessible from Public Project → Agents → Admin tab/section
- List of currently published agents visible with details (name, author, publish date, version)
- Upload/Publish button available in Admin section
- Admin can upload an agent config directly
- Agent appears in Agents Studio immediately after admin publish
- AI validation dialog/checks are NOT triggered during admin upload
- Agent with incomplete metadata (would fail AI validation) can still be published by admin

## Preconditions

- Logged in as Platform Admin on {{base_url}}
- Access to Public Project
- Incomplete agent config file prepared (agent with no description and using generic name like "New Agent")

## Test Data

- Public Project name/ID: note from environment
- Incomplete agent config file: exported agent JSON/YAML missing description and using generic name "New Agent"
- Expected published agent name: as defined in the config file

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Public Project in ELITEA (use project switcher in the sidebar) | Public Project loads |
| 2 | Click on the Agents menu in the sidebar | Agents list for Public Project loads |
| 3 | Look for an "Admin" tab or section within the Agents view | Admin section/tab is visible (only visible to Platform Admin) |
| 4 | Click the Admin section | Admin page opens; a list of currently published agents is shown |
| 5 | Verify the published agents list shows: agent name, author, publish date, version | All four details are present for each listed agent |
| 6 | Locate and click the "Upload/Publish" button | An upload dialog or form opens |
| 7 | Upload the incomplete agent config file (no description, generic name) | File is accepted by the upload dialog |
| 8 | Confirm the upload/publish action | Publish proceeds without showing any AI validation dialog, error, or warning about missing description or generic name |
| 9 | Navigate to Agents Studio | The uploaded agent appears in Agents Studio listing |
| 10 | Verify the agent is searchable and startable | Agent is findable by its name; a new conversation can be started |

## Expected Final State

Agent is findable by its name; a new conversation can be started

## Pass/Fail Criteria

**Pass:**
- Admin section is accessible from Public Project → Agents
- Published agents list shows name, author, publish date, version
- Upload/Publish flow completes without any AI validation checks or dialogs
- Agent with incomplete metadata is published successfully
- Published agent appears immediately in Agents Studio

**Fail:**
- Admin section is not visible or accessible for a Platform Admin
- AI validation dialog appears during admin upload flow
- Incomplete agent config is rejected due to quality/validation rules
- Published agent does not appear in Agents Studio after admin upload

---
id: ELITEA-0155
title: "Chat — Correct version-specific icons shown when selecting a specific published version (multi-version agent, including sub-agents)"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agent-publishing, feat:agent-studio, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4670]
---
# ELITEA-0155: Chat — Correct version-specific icons shown when selecting a specific published version (multi-version agent, including sub-agents)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an agent has multiple published versions each with a different icon, selecting a specific version in Chat shows that version's correct icon, and sub-agents also show their correct icons.

**Coverage:**
- Per-version icon rendering in Chat when a specific version is selected
- Icon accuracy across multiple published versions with different icons
- Sub-agent icon display when parent agent references sub-agents

## Preconditions

- Logged in to ELITEA
- An agent with at least 2 published versions, each with a different icon (e.g., version "v1" with image_1.png, version "v-tiff" with 3006bec5....png)
- Navigate to Chat

## Test Data

| Version | icon_meta.name |
|---|---|
| v1 | image_1.png |
| v-tiff | 3006bec5-46e7-448b-9464-55d9fa4a1171.png |
| Sub-agent | any published agent with a known icon |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and add the multi-version agent | Agent appears in chat |
| 2 | Select version "v1" in Chat | Icon for "v1" (image_1.png) is displayed |
| 3 | Switch to version "v-tiff" in Chat | Icon updates to the "v-tiff" icon (3006bec5....png) |
| 4 | If the agent uses a sub-agent: run the agent with a prompt that invokes the sub-agent | Sub-agent icon is displayed correctly in Chat |
| 5 | Confirm all icons match the selected version's icon_meta.url | Each version shows its own icon; no fallback shown |

## Expected Final State

Each version shows its own icon; no fallback shown

## Pass/Fail Criteria

**Pass:**
- Each version shows its own distinct icon; switching versions updates the icon
- Sub-agent icons displayed correctly

**Fail:**
- Wrong version's icon shown after switching
- Fallback icon shown when a specific icon exists
- Sub-agent shows fallback icon

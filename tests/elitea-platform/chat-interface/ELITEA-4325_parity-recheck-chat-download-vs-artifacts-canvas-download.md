---
id: ELITEA-4325
title: "Parity Re-check: Chat Code Block Download Does Not Regress Artifacts/Canvas MDX Download Pattern"
priority: high
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:artifacts, feat:canvas, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- User has access to Artifacts/Canvas with an existing or newly created MDX file
- This is a regression re-check against existing Canvas/Artifacts cases ELITEA-3865 (Copy Content from Three-Dot Menu), ELITEA-3866 (Download MDX File from Three-Dot Menu), and ELITEA-3868 (MDX Syntax Highlighting in Raw Mode) - the checklist's closest existing analog to this new chat feature

## Test Data

| Field | Value |
|-------|-------|
| URL (chat) | `{{base_url}}/app/chat` |
| URL (artifacts/canvas) | `{{base_url}}/app/artifacts` (or equivalent Canvas entry point) |
| Chat prompt | "Give me a short json config example" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In chat, send the prompt and confirm a code block with a working Download icon appears (sanity check, not the main focus of this case) | Download icon present and functional on the chat code block, consistent with ELITEA-4317 |
| 2 | Navigate to Artifacts, open an existing `.mdx` file in Canvas | File opens in Canvas editor |
| 3 | Re-run ELITEA-3865: click the three-dot menu and select "Copy Content" | MDX source is copied to clipboard without error, exactly as before the chat feature shipped |
| 4 | Re-run ELITEA-3866: click the three-dot menu and select "Download" | File downloads with the correct `.mdx` extension and content matching the Canvas source, exactly as before the chat feature shipped |
| 5 | Re-run ELITEA-3868: switch the MDX file to Raw mode | Raw mode still displays proper MDX/Markdown syntax highlighting, unaffected by any shared toolbar/download component changes introduced for chat |
| 6 | Compare the Canvas three-dot "Download" entry point and resulting filename/extension pattern against the chat code block's inline Download icon and its filename/extension pattern | The two download mechanisms remain visually and functionally distinct entry points (three-dot menu on a whole file vs. inline icon on a code block); no UI regression, crossover, or shared-state bug is observed in either |

## Expected Final State

The pre-existing Canvas/Artifacts MDX copy, download, and raw-mode syntax highlighting behaviors (ELITEA-3865/3866/3868) are confirmed unaffected by the introduction of the new chat code-block Download feature, and the two download mechanisms remain cleanly separated.

## Pass/Fail Criteria

**Pass:**
- ELITEA-3865, ELITEA-3866, and ELITEA-3868 all pass exactly as previously defined, with no behavioral change
- The Canvas three-dot Download entry point and the chat inline code-block Download icon remain independent, non-interfering features

**Fail:**
- Any regression is observed in ELITEA-3865/3866/3868 behavior (copy, download, or raw-mode highlighting) traceable to shared component changes from the new chat feature
- The two download mechanisms show any crossover, shared-state bug, or visual confusion

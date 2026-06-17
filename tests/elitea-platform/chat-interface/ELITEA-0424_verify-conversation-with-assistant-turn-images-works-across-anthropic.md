---
id: ELITEA-0424
title: "Verify Conversation With Assistant-Turn Images Works Across Anthropic and GPT Models [Parametrized]"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, feat:attachments, eng:backend, feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3910]
---
# ELITEA-0424: Verify Conversation With Assistant-Turn Images Works Across Anthropic and GPT Models [Parametrized]

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after an image-generation tool produces an image in an assistant turn, sending follow-up messages in the same conversation succeeds without errors — across all tested models and across both Agent Chat and direct Chat pages.

**Coverage:**
- Image generation completes successfully in the assistant turn
- Follow-up messages are processed correctly when chat history contains an assistant-turn image
- All tested GPT and Anthropic models handle the conversation without errors
- Behavior is consistent on both Agent Chat and direct Chat pages

## Preconditions

- Logged in to {{base_url}}
- An Chat and Agent with an **image-generation toolkit enabled** is available
- The target model for each row is configured and selectable in the conversation
- Skip any model row whose model is not available on the test environment

## Test Data

Run the full step sequence for each combination of Page and Model below. Skip any model row not available on the test environment.

**Pages:**
| # | Page | Navigation |
|---|------|------------|
| A | Agent Chat | Sidebar → Agents → open Agent with image-generation toolkit → Chat tab |
| B | Direct Chat | Sidebar → Projects → select a project → Chat → add the image-generation agent |

**Models:**
| # | Model |
|---|-------|
| 1 | GPT-5 mini or GPT-5.2 (or any available GPT model) |
| 2 | Anthropic Claude 3.7 Sonnet |
| 3 | Anthropic Claude Haiku 4.5 |
| 4 | Anthropic Claude 4.5 Sonnet or 4.6 Sonnet (whichever is available) |
| 5 | Anthropic Claude Opus 4.5 or 4.6 (whichever is available; skip if absent) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the target page (A or B) and open a new conversation with the image-generation agent. Select the target model for this iteration. | Conversation opens on the correct page with the correct model active. |
| 2 | Send: "Generate an image of a mountain landscape. Without clarifications." | Agent invokes the image-generation tool. An image is generated and displayed in the assistant reply. |
| 3 | Confirm the image is visible inside the assistant turn in chat history. | Image renders correctly. No errors. |
| 4 | Send a follow-up: "Describe the image you just generated." | A valid text response is returned. No error appears. |
| 5 | Send a second follow-up: "What colors are dominant in that image?" | Another valid response is returned. The conversation continues without errors. |
| 6 | Repeat Steps 1–5 for the next model row using a fresh conversation on the same page. Once all model rows are done for Page A, repeat all rows for Page B. | All combinations complete successfully. |

## Expected Final State

All combinations complete successfully.

## Pass/Fail Criteria

**Pass:**
- All tested model and page combinations produce valid responses on both follow-up messages (Steps 4–5)
- No error appears during or after image generation in any combination

**Fail:**
- Any model or page combination returns an error on a follow-up message
- The conversation becomes inoperable after the image is generated in any combination

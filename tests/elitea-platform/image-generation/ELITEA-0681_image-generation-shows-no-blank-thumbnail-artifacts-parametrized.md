---
id: ELITEA-0681
title: "Image Generation Shows No Blank Thumbnail Artifacts [Parametrized]"
priority: high
type: functional
module: image-generation
status: draft
execution_type: manual
tags: [feat:image-generation, rca:regression, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3936]
---
# ELITEA-0681: Image Generation Shows No Blank Thumbnail Artifacts [Parametrized]

**Module:** Image Generation · **Priority:** High · **Type:** Functional

**Objective:** Verify that image generation shows only the generated image — no blank or corrupted thumbnail artifacts — across GPT, Anthropic, and other supported models, from both Chat and Agent pages.

**Coverage:**
- No blank/corrupted thumbnail appears alongside the generated image for any tested model
- GPT 5.2 (gpt-image-1), Anthropic, and other image-generation models all produce clean results
- Behavior is consistent across all model types
- Behavior is consistent across both Chat page and Agent chat page

## Preconditions

- Logged in to the ELITEA platform at {{base_url}}
- Browser: Chrome (latest stable)
- Image generation is enabled in the project
- GPT 5.2 (gpt-image-1), at least one Anthropic image-capable model, and optionally one other model type are available
- An agent with Image Generation toolkit enabled exists (for Agent page testing)

## Test Data

| # | Model | Provider |
|---|---|---|
| 1 | gpt-image-1 (GPT 5.2) | OpenAI |
| 2 | Any Anthropic image-capable model | Anthropic |
| 3 | Any other available image-generation model | Other |

Prompt: `Create an image of a dog`
Pages to test: Chat page, Agent chat page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Go to Chat. Enable Image Generation and select gpt-image-1 (GPT 5.2). Send the prompt: "Create an image of a dog". | The generated image appears. No blank or corrupted thumbnail is shown alongside it. |
| 2 | Repeat step 1 using an Anthropic image-capable model. | The generated image appears. No blank or corrupted thumbnail is shown. |
| 3 | If a third model type is available, repeat with that model. | The generated image appears. No blank or corrupted thumbnail is shown. |
| 4 | Navigate to the Agent page. Open an agent with Image Generation enabled. Select gpt-image-1 (GPT 5.2) and send the prompt: "Create an image of a dog". | The generated image appears in the agent chat. No blank or corrupted thumbnail is shown alongside it. |
| 5 | Repeat step 4 using an Anthropic image-capable model. | The generated image appears. No blank or corrupted thumbnail is shown. |
| 6 | If a third model type is available, repeat with that model on the Agent page. | The generated image appears. No blank or corrupted thumbnail is shown. |

## Expected Final State

The generated image appears. No blank or corrupted thumbnail is shown.

## Pass/Fail Criteria

**Pass:**
- Generated image displays correctly for all tested models on both Chat and Agent pages
- No blank, empty, or corrupted thumbnail appears alongside the image in any context
- Behavior is consistent across GPT 5.2, Anthropic, and any other tested model

**Fail:**
- A blank or corrupted thumbnail appears next to the generated image for any model or page
- No image is generated at all
- Artifact behavior differs between model types or between Chat and Agent pages

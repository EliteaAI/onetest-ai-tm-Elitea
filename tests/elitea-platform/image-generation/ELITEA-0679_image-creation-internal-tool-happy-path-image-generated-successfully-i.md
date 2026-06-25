---
id: ELITEA-0679
title: "Image Creation Internal Tool — Happy Path: Image Generated Successfully in Chat and Agent"
priority: critical
type: functional
module: image-generation
status: ready
execution_type: automated
automation_test_id:
  - test_image_creation.py:TestImageCreation.test_create_image
tags: [feat:image-generation, feat:chat, r-2.0.3]
requirements: []
---
# ELITEA-0679: Image Creation Internal Tool — Happy Path: Image Generated Successfully in Chat and Agent

**Module:** Image Generation · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the image creation internal tool generates and displays an image successfully — from both the Chat page and the Agent chat page — using the default image model.

**Coverage:**
- Image Creation internal tool enabled and image generated in Chat
- Image Creation internal tool enabled and image generated in Agent chat
- Generated image is displayed in the conversation without errors

## Preconditions

- At least one shared image model is available as the default
- The user has access to Chat and has at least one Agent configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat and create a new conversation | Chat input is ready |
| 2 | Open the internal tools settings and enable the Image Creation tool | Image Creation tool is toggled ON |
| 3 | Send a simple image prompt (e.g., "Generate an image of a sunset over the ocean") using the default image model | The generated image is displayed in the chat — no error, no 400 response, no 'Invalid model name' message |
| 4 | Navigate to an Agent, open its chat panel, and enable the Image Creation internal tool | Image Creation tool is toggled ON in the Agent context |
| 5 | Send the same image prompt in the Agent chat using the default image model | The generated image is displayed in the Agent chat — no error, no 400 response, no 'Invalid model name' message |

## Expected Final State

The generated image is displayed in the Agent chat — no error, no 400 response, no 'Invalid model name' message

## Pass/Fail Criteria

PASS: Image renders correctly in both Chat and Agent chat with no errors
FAIL: Any error returned (e.g., "Invalid model name", 400); image not displayed in either context

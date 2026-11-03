---
id: ELITEA-4388
title: "Mermaid Diagrams and Markdown Tables Do Not Display a Broken or Partial Download Control"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- User has access to a Private project
- Mermaid diagrams and Markdown tables are rendered via components separate from standard fenced code blocks and are not an intended target of the new Download control (per implementation notes); this case re-validates they are not incidentally/incorrectly affected
- Touchpoint vs ELITEA-2088 (chat generate Mermaid diagram and open in Canvas mode)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt (Mermaid) | "Generate a simple Mermaid flowchart diagram showing a 3-step approval process" |
| Prompt (Markdown table) | "Give me a markdown table comparing three programming languages by typing, performance, and ecosystem" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and open a direct chat conversation | Chat page loads |
| 2 | Send the Mermaid prompt and wait for the response | AI responds with a message rendering a Mermaid diagram (re-validation touchpoint vs ELITEA-2088) |
| 3 | Inspect the toolbar/controls associated with the rendered Mermaid diagram | No Download icon is shown on the Mermaid diagram's controls, OR if a Download-like icon is shown, it is fully functional (produces a valid file) rather than broken, disabled-looking, or erroring when clicked |
| 4 | If the Mermaid diagram offers an "open in Canvas" action, trigger it and confirm Canvas opens normally | Canvas opens with the diagram rendered correctly, unaffected by the new chat code-block Download feature |
| 5 | Send the Markdown table prompt and wait for the response | AI responds with a message rendering a Markdown table |
| 6 | Inspect the toolbar/controls associated with the rendered Markdown table | No Download icon is shown on the Markdown table, OR if shown, it is fully functional rather than broken or non-functional |
| 7 | If either the Mermaid diagram or Markdown table unexpectedly shows a Download icon, click it and inspect the result | Either a valid file downloads with sensible content, or the control is confirmed absent/inactive; no console error, broken icon state, or non-responsive click occurs |

## Expected Final State

Mermaid diagrams and Markdown tables rendered in chat responses show no broken, partial, or non-functional Download control; the new per-code-block Download feature either correctly excludes these content types or, if present, behaves correctly for them.

## Pass/Fail Criteria

**Pass:**
- No Download icon appears on Mermaid diagrams or Markdown tables, or if present, it is fully functional
- No console error, broken icon, or unresponsive click is observed on either content type
- Mermaid's existing "open in Canvas" behavior (ELITEA-2088) remains unaffected

**Fail:**
- A Download icon appears on a Mermaid diagram or Markdown table but is non-functional, errors, or produces corrupted/empty output
- The Mermaid-to-Canvas flow regresses as a result of shared toolbar/component changes

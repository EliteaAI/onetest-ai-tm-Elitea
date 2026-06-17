---
id: ELITEA-0134
title: "Swarm Agent - Thought/Action Accordion Display with GPT Models"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0134: Swarm Agent - Thought/Action Accordion Display with GPT Models

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that thought/action accordion UI elements display correctly in swarm agent chat when GPT models (GPT-4.5, GPT-5) are used.

## Preconditions

User logged into Elitea stage.elitea.ai\nSwarm agent with child agents exists\nGPT-4.5 and GPT-5 models available in model selector

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a swarm agent configured with GPT-4.5 model | Swarm agent created with GPT-4.5 model selected |
| 2 | Add at least one child agent with a configured toolkit | Child agent associated with parent swarm agent |
| 3 | Open the swarm agent chat and send a request that triggers child agent invocation | Chat processes the request and invokes child agent |
| 4 | Observe the chat output for thought/action accordion elements (.MuiAccordion-root) | Thought/action accordions are displayed showing reasoning steps and tool calls |
| 5 | Click on the accordion to expand it and verify content | Accordion expands showing detailed thought process and action results |
| 6 | Verify that the accordion content includes specific fields: thought text, action name, action input parameters, and observation/result output | All accordion fields are present and populated with meaningful data — no empty or placeholder values |
| 7 | Collapse the accordion and verify it returns to its compact state without losing content, then re-expand to confirm persistence | Accordion collapses and re-expands correctly with all content preserved; no data loss on toggle |
| 8 | Repeat steps 1-7 with GPT-5 model configured | Accordions display identically with GPT-5 model — same fields, same layout, same expand/collapse behavior |
| 9 | For comparison, repeat with a Claude model to verify accordion works on non-GPT models | Accordions display correctly with Claude model (baseline comparison) |
| 10 | Send a request that does NOT trigger child agent invocation (simple question answerable by the parent agent alone) and verify no false accordion elements appear | No thought/action accordions are displayed when child agent is not invoked — accordion only appears for actual tool/sub-agent calls |
| 11 | Send multiple rapid requests (3-4 messages quickly) that each trigger child agent invocation and verify each response has its own independent accordion | Each response has its own correctly rendered accordion with distinct content; no accordion content mixing between responses or missing accordions on any response |

## Expected Final State

Each response has its own correctly rendered accordion with distinct content; no accordion content mixing between responses or missing accordions on any response

## Pass/Fail Criteria

Accordion elements (.MuiAccordion-root) visible in chat output for GPT models
Accordion expandable with thought/action content including thought text, action name, input params, and observation
No difference in accordion rendering between GPT and non-GPT models
Accordion toggle (collapse/expand) preserves content
No false accordion elements when child agent is not invoked
Multiple rapid requests produce independent, correctly rendered accordions

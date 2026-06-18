---
id: ELITEA-1348
title: "Fixed USER MESSAGE: Static Text Displayed Verbatim Regardless of Pipeline State"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1348: Fixed USER MESSAGE: Static Text Displayed Verbatim Regardless of Pipeline State

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that when USER MESSAGE type is Fixed, the configured static text is always displayed verbatim to the reviewer, regardless of pipeline input values.

**Coverage:**
- Fixed text displayed unchanged
- No unexpected variable substitution on Fixed type
- Consistent output across multiple runs

## Preconditions

- Pipeline with HITL node; USER MESSAGE type = Fixed; value = 'Please approve or reject this content.'
- Pipeline runnable in Chat interface

## Test Data

Expected USER MESSAGE: Please approve or reject this content.; Run input 1: Document A; Run input 2: Document B

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm HITL configuration: USER MESSAGE type = Fixed, value = 'Please approve or reject this content.' | Configuration verified |
| 2 | Run the pipeline with input 'Document A' | Pipeline pauses at HITL; USER MESSAGE = 'Please approve or reject this content.' |
| 3 | Run the pipeline again with input 'Document B' | USER MESSAGE still = 'Please approve or reject this content.' — unchanged |
| 4 | Confirm no variable references substituted | Text is exactly as configured; no dynamic parts |

## Expected Final State

Text is exactly as configured; no dynamic parts

## Pass/Fail Criteria

**Pass:**
- Fixed text is identical on every run regardless of input
- No substitution occurs

**Fail:**
- Text changes between runs
- Variable-style substitution occurs on Fixed type

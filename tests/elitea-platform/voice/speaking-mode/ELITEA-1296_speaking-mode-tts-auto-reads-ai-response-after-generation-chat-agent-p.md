---
id: ELITEA-1296
title: "Speaking Mode — TTS Auto-Reads AI Response After Generation [Chat, Agent, Pipeline]"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1296: Speaking Mode — TTS Auto-Reads AI Response After Generation [Chat, Agent, Pipeline]

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify TTS audio starts automatically once the AI response is fully received — no user interaction needed — on Chat, Agent, and Pipeline pages.

**Coverage:** Auto-TTS starts after response arrives; audio matches response; works on all 3 pages.

## Preconditions

- Speaking Mode active; speakers/headphones functional

## Test Data

Request: "What are three benefits of exercise?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode on Chat. Speak: "What are three benefits of exercise?" — let it auto-send. | Response generated |
| 2 | After response appears, observe audio — do not click anything. | TTS plays automatically; audio matches response text |
| 3 | Repeat steps 1–2 on the Agent page. | TTS auto-reads on Agent page |
| 4 | Repeat steps 1–2 on the Pipeline page. | TTS auto-reads on Pipeline page |

## Expected Final State

TTS auto-reads on Pipeline page

## Pass/Fail Criteria

**Pass:**
- TTS starts automatically on all 3 pages without any button click

**Fail:**
- TTS does not start automatically; manual Read Out required on any page

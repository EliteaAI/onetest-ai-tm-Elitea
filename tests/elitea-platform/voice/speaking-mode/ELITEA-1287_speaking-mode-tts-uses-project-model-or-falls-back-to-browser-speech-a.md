---
id: ELITEA-1287
title: "Speaking Mode — TTS Uses Project Model or Falls Back to Browser Speech API"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1287: Speaking Mode — TTS Uses Project Model or Falls Back to Browser Speech API

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify TTS uses the project-configured model when available and falls back to the browser's native Speech API when no project TTS model is set.

**Coverage:** Project A (configured model) → project voice used; Project B (no model) → browser fallback used; TTS plays in both cases.

## Preconditions

- Two project contexts available: Project A with TTS model configured, Project B with no TTS model set

## Test Data

Project A: TTS model configured. Project B: no TTS model. Request: "Explain the water cycle briefly"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Project A (TTS model configured). Enable Speaking Mode. Speak: "Explain the water cycle briefly". Let auto-send and TTS play. | TTS uses project model voice (as configured) |
| 2 | Navigate to Project B (no TTS model). Enable Speaking Mode. Speak the same request. | TTS plays using the browser Speech API (different voice from Project A); no error |

## Expected Final State

TTS plays using the browser Speech API (different voice from Project A); no error

## Pass/Fail Criteria

**Pass:**
- Project A uses project model voice; Project B uses browser Speech API (audibly different); TTS plays successfully in both

**Fail:**
- Project B throws an error instead of falling back; same voice in both projects; TTS silent in either

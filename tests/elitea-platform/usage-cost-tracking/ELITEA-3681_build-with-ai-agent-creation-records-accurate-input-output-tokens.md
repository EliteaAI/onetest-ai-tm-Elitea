---
id: ELITEA-3681
title: "Build with AI (Agent creation) records accurate input/output tokens and surfaces in Analytics within ~5 min"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, build-with-ai, agents]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6568", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3681: Build with AI (Agent creation) records accurate input/output tokens and surfaces in Analytics within ~5 min

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that invoking "Build with AI" from the Agent creation `GenerateAgentModal` produces a `usage_event` row with accurate input/output token counts, and that the row surfaces in Analytics/Costs within ~5 minutes.

---

## Preconditions

- Logged in to {{base_url}} as a user with admin or editor role (Build with AI is hidden for viewer).
- A runtime interface (LiteLLM or WAM) is configured and capturing LLM usage per #6571/#6607.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent description (NL input) | "A customer support agent that answers billing questions using the knowledge base" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents → Create Agent → click "Build with AI" to open `GenerateAgentModal`. | Modal opens with a natural-language description field. |
| 2 | Enter the test description and submit. | LLM generates a full agent draft: name, instructions, suggested resources, suggested skills (up to 5). |
| 3 | Record the exact text of the description sent and the full generated draft returned. | Both are available for token-count comparison. |
| 4 | Approve/create the agent from the draft. | Agent is created successfully. |
| 5 | Within 5 minutes, navigate to Analytics → Costs (or query `usage_event` directly if accessible). | A row for this invocation is present. |
| 6 | Verify input tokens on the row reflect the natural-language description sent to the LLM. | Input token count is non-zero and proportionate to the description length (not 0, not a placeholder). |
| 7 | Verify output tokens on the row reflect the generated draft (instructions + suggested resources/skills). | Output token count is non-zero and proportionate to the draft size. |

---

## Expected Final State

A single `usage_event` row exists for the Build-with-AI invocation with non-zero, plausible input and output token counts, visible in Analytics within ~5 minutes.

---

## Pass/Fail Criteria

**Pass:**
- Row appears in `usage_event`/Analytics within ~5 minutes of the call.
- Input tokens reflect the description sent; output tokens reflect the generated draft; neither is 0 or missing.

**Fail:**
- No row appears within 5 minutes.
- Input or output tokens are 0, missing, or clearly inconsistent with the actual payload sizes.

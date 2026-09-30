---
id: ELITEA-3206
title: "Viewer Role Access to Own Private Secret — Record Actual Behavior (Open Question)"
priority: medium
type: negative
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, viewer-role, open-question]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3206: Viewer Role Access to Own Private Secret — Open Question

**Module:** Pipelines / Code Node · **Priority:** Medium · **Type:** Negative

**Objective:** Design notes list `configuration.secrets.secret.unsecret` as `viewer: False`, which would suggest a Viewer cannot resolve even their own private secret via a code node. This is called out as an open question rather than a locked design decision — this case exists to record the actual observed behavior so the ambiguity can be resolved with a concrete answer instead of an assumption.

**Coverage:** Extra — Viewer role open question

**Note:** Pass/Fail is not applicable in the usual sense — record the result as a finding. If a Viewer's own private secret is unreachable, confirm whether that's the intended design (raise as a UX question if it seems unintentional, since it's the Viewer's *own* personal secret, not someone else's). If it *is* reachable, confirm no other Viewer-role restriction is silently bypassed by this path.

## Preconditions

- A user with Viewer role on the relevant project
- That same user has a personal project with a shared personal secret `AQA_TOKEN`
- A pipeline/code node the Viewer can trigger (e.g. via a manual run they're permitted to start, if any)

## Code Node

```python
try:
    value = elitea_client.get_private_project_secret('AQA_TOKEN')
    test_results = {"error": None, "resolved": value is not None}
except Exception as e:
    test_results = {"error": type(e).__name__, "resolved": False}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As the Viewer-role user, trigger the code node above against their own shared personal secret. | Record whether the call succeeds or raises. |
| 2 | If it raises, capture the exact error type/message. | Documented for follow-up. |
| 3 | If it succeeds, confirm the returned value is genuinely the Viewer's own secret (not someone else's, not a leak). | Documented for follow-up. |

## Expected Final State

The actual current behavior (permitted or refused) is documented as a finding, with a note on whether it matches the `viewer: False` permission note or contradicts it.

## Finding template

- Observed behavior: `<succeeded / raised — error type>`
- Matches `viewer: False` expectation: `<yes / no>`
- Recommended follow-up: `<none — working as designed / raise as UX question — Viewer blocked from own secret / raise as bug — Viewer got someone else's value>`

---
name: R7385Failer
description: 'Test data for #7385: needs 6 tool steps but has a step limit of 3, so the run fails.'
model: global.anthropic.claude-sonnet-5-5
max_tokens: -1
agent_type: agent
step_limit: 3
toolkits:
- toolkit: r7385_echo
  type: openapi
  settings:
    base_url: https://postman-echo.com
    openapi_configuration: {}
    spec: |
      openapi: 3.0.3
      info:
        title: Postman Echo delay (R7385 fixture)
        version: "1.0"
        description: >-
          Public, no auth. GET /delay/{seconds} answers after that many seconds (0-10), which gives the
          R7385 agents a deterministic latency knob.
      servers:
        - url: https://postman-echo.com
      paths:
        /delay/{seconds}:
          get:
            operationId: waitSeconds
            summary: Wait the given number of seconds (0-10) and return {"delay":"<seconds>"}.
            parameters:
              - name: seconds
                in: path
                required: true
                schema:
                  type: integer
                  minimum: 0
                  maximum: 10
            responses:
              "200":
                description: Waited
  tools:
  - waitSeconds
- toolkit: r7385_jph
  type: openapi
  settings:
    base_url: https://jsonplaceholder.typicode.com
    openapi_configuration: {}
    spec: |
      openapi: 3.0.3
      info:
        title: JSONPlaceholder (R7385 fixture)
        version: "1.0"
        description: >-
          Static fake REST data. Users 1-10 and posts 1-100 exist; any other id returns 404,
          which gives a deterministic tool error.
      servers:
        - url: https://jsonplaceholder.typicode.com
      paths:
        /users/{id}:
          get:
            operationId: getUser
            summary: Get one user by numeric id (1-10). Returns name, username, email, company.
            parameters:
              - name: id
                in: path
                required: true
                schema:
                  type: integer
            responses:
              "200":
                description: The user
              "404":
                description: No such user
        /posts/{id}:
          get:
            operationId: getPost
            summary: Get one blog post by numeric id (1-100). Returns userId (the author's user id), title, body.
            parameters:
              - name: id
                in: path
                required: true
                schema:
                  type: integer
            responses:
              "200":
                description: The post
              "404":
                description: No such post
  tools:
  - getPost
  - getUser
---

You are a test fixture for a chat run that fails. Follow these steps exactly, in order, one tool call per turn:

1. Call waitSeconds with seconds = 10.
2. Call getPost with id 1.
3. Call getPost with id 2.
4. Call getPost with id 3.
5. Call getPost with id 4.
6. Call getPost with id 5.
7. Answer `FAIL-DONE` (you should never get here: your step limit is lower than the number of steps).

Never skip a step, and never ask the user anything.

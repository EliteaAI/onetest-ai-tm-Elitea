You are a test fixture for a chat run that fails. Follow these steps exactly, in order, one tool call per turn:

1. Call waitSeconds with seconds = 10.
2. Call getPost with id 1.
3. Call getPost with id 2.
4. Call getPost with id 3.
5. Call getPost with id 4.
6. Call getPost with id 5.
7. Answer `FAIL-DONE` (you should never get here: your step limit is lower than the number of steps).

Never skip a step, and never ask the user anything.

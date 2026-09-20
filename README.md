# Aurora Paper Executor

Public execution shell for **Portfolio Autónomo #2**.

This repository intentionally contains no trading state, order journal, Alpaca
credentials, portfolio decisions, or strategy memory. Its only job is to provide
free standard GitHub-hosted runner capacity and execute the trusted bridge stored
in the private repository `gomez5757/aurora-swing-paper`.

## Trigger

Only a newly created comment by `gomez5757` on Issue #1 whose body is exactly:

```text
/run p2
```

starts the executor.

The workflow checks out the private repository with a private repository token,
runs its tests, fabricates a safe private `workflow_dispatch` context, and then
runs `python -m p2_bridge.run`.

All commands, receipts, state and journals remain in the private repository.

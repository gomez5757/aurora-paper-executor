# Aurora Paper Executor

Public, **secret-free execution shell** for the private Aurora Alpaca Paper bridge.

This repository provides standard GitHub-hosted runner capacity for both autonomous paper portfolios while all strategy, trading state, receipts, journals and command payloads remain in the private repository `gomez5757/aurora-swing-paper`.

## Public trigger bus

Issue #1 accepts only owner comments:

```text
/selftest p1
/run p1
/selftest p2
/run p2
```

The public comments never contain broker commands, positions, account data or receipts.

## Isolation

Portfolio #1:
- private queue: `queue_p1/`
- private state: `state/current.json`
- private journal: `journal/`

Portfolio #2:
- private queue: `queue_p2/`
- private state: `state/portfolio2.json`
- private journal: `journal_p2/`

A repository-scoped deploy key allows this executor to clone and persist results back to the private Aurora repository. Alpaca credentials, when configured, exist only as encrypted Actions secrets in this executor repository.

The user's local PC is not part of runtime execution.

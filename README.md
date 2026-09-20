# Aurora Paper Executor

Public, secret-free execution shell for **Portfolio Autónomo #2**.

## What is public here

Only:
- the runner workflow;
- this documentation;
- Issue #1 trigger comments such as `/selftest p2` and `/run p2`.

Never put trading commands, positions, receipts, account data or credentials in this repository.

## What remains private

`gomez5757/aurora-swing-paper` keeps:
- `PORTFOLIO_2.md` and the operating protocol;
- `state/portfolio2.json`;
- `queue_p2/`;
- `journal_p2/`;
- Portfolio #2 memory in private Issue #10.

The public workflow checks out the private repository with a repository-scoped,
write-enabled deploy key stored as the encrypted secret
`AURORA_PRIVATE_SSH_KEY`. The deploy key cannot access other repositories.

## Commands

On public Issue #1:

```text
/selftest p2
```

Runs checkout + install + full private test suite + Python compilation + a
no-mutation `git push --dry-run`.

```text
/run p2
```

Does the same verification and then drains `queue_p2/pending/`.

Broker execution additionally requires encrypted repository secrets:

- `ALPACA_P2_API_KEY_ID`
- `ALPACA_P2_API_SECRET_KEY`

The workflow is restricted to triggers created by GitHub user `gomez5757`.

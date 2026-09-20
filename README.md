# Aurora Paper Executor

Public, secret-free execution shell for the private Aurora Alpaca Paper bridge.

This repository provides standard GitHub-hosted runner capacity for both autonomous **Paper** portfolios while strategy, trading state, receipts, journals and command payloads remain in the private repository `gomez5757/aurora-swing-paper`.

## Public trigger bus

Issue #1 accepts only owner comments:

```text
/selftest p1
/run p1
/selftest p2
/run p2
```

The public comments never contain broker commands, positions, account data or receipts.

## Broker authentication

Portfolio #1 and Portfolio #2 use **separate Alpaca Paper OAuth authorizations**.

- P1 encrypted profile: `auth/p1.oauth.sealed` in the private repository.
- P2 encrypted profile: `auth/p2.oauth.sealed` in the private repository.
- The profiles contain only Alpaca Paper OAuth grants and are encrypted with libsodium sealed boxes.
- The matching decrypt key exists only as the encrypted GitHub Actions secret `AURORA_OAUTH_BOX_PRIVATE_KEY_B64` in this executor.
- The runner decrypts the selected profile in memory and sends `Authorization: Bearer ...` to Alpaca.
- The private bridge remains hard-pinned to `https://paper-api.alpaca.markets`.

No Alpaca API key/secret pair is required by the normal public-executor path.

## Isolation

Portfolio #1:
- private queue: `queue_p1/`
- private state: `state/current.json`
- private journal: `journal/`
- OAuth authorization: P1 Paper account only

Portfolio #2:
- private queue: `queue_p2/`
- private state: `state/portfolio2.json`
- private journal: `journal_p2/`
- OAuth authorization: P2 Paper account only

A repository-scoped deploy key allows this executor to clone and persist results back to the private Aurora repository.

The user's local PC is not part of runtime execution.

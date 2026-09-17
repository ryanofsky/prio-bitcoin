---
title: Tools and scripts
owner: ryanofsky
labels: ["Scripts and tools"]
paths: ["contrib/", "src/bitcoin-tx", "src/bitcoin-util", "src/bitcoin-wallet", "src/bitcoin-chainstate", "src/bitcoin.cpp", "test/get_previous_releases.py", "contrib/seeds", "contrib/signet", "contrib/tracing", "contrib/message-capture", "contrib/linearize"]
keywords: ["bitcoin-tx", "bitcoin-util", "bitcoin-wallet tool", "contrib", "seeds", "signet", "tracing", "usdt", "script", "tool", "linearize", "message capture", "asmap"]
---

## Covers

Command-line tools other than the node and its RPC client, and the
scripts under contrib: `bitcoin-tx`, `bitcoin-util`, the offline
`bitcoin-wallet` tool, the `bitcoin` wrapper, seed and asmap
generation, signet tooling, tracing scripts, and developer helper
scripts. Build and release scripts are build; test helpers are tests.
The Scripts and tools label is a strong prior.

## What matters here

Tools that operators and downstream projects depend on first: seed
generation, asmap, signet, and the wallet tool affect real deployments.
Then correctness of any tool that touches keys or transactions. Then
developer productivity tools that many contributors use. Then niche or
single-user scripts, which rank low regardless of size.

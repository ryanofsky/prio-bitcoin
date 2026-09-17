---
title: Mining
owner: ryanofsky
labels: ["Mining"]
paths: ["src/node/miner", "src/interfaces/mining", "src/ipc/capnp/mining", "src/rpc/mining", "src/bitcoin-mine", "test/functional/mining_", "test/functional/interface_ipc"]
keywords: ["mining", "block template", "getblocktemplate", "BlockAssembler", "waitNext", "template manager", "stratum", "sv2", "coinbase", "bitcoin-mine"]
---

## Covers

Block template construction and everything a miner or pool interacts
with: the block assembler, `getblocktemplate` and related RPCs, the
`Mining` interface and its IPC exposure, template update logic (fee
inflow, new tip, waitNext), the `bitcoin-mine` program, and the tests
for these. A mining PR that adds or changes an `interfaces::Mining`
method or its capnp definition is mining first and ipc second. The
Mining label is a strong prior.

Not mining: general IPC infrastructure that the mining interface happens
to use (that is ipc); mempool policy that affects which transactions are
eligible (that is mempool).

## What matters here

Template validity above all: a template that produces an invalid block
loses the block reward. Then correctness of fee and weight accounting,
and of template updates as the mempool and tip change. Then latency and
resource use of template generation, which pools feel per block. Then
completeness and stability of the interface external miners build on
(Stratum v2 template providers are the current consumer). Then
developer-facing tooling.

Changes whose benefit is a small fraction of a block's fees, weighed
against any risk of invalidity, rank low; say so with the numbers when
the discussion has them.

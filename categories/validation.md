---
title: Validation
owner: ryanofsky
labels: ["Validation", "Consensus", "Block storage", "UTXO Db and Indexes", "Kernel"]
paths: ["src/validation", "src/consensus", "src/kernel", "src/node/blockstorage", "src/node/chainstate", "src/coins", "src/txdb", "src/chain", "src/script/interpreter", "src/primitives"]
keywords: ["validation", "consensus", "chainstate", "reorg", "IBD", "assumeutxo", "kernel", "libbitcoinkernel", "block index", "coins cache", "utxo"]
---

## Covers

Block and transaction validation, consensus rules and their
implementation, chainstate and block-index management, the UTXO set and
its cache and database, block storage, reorg handling, initial block
download and assumeutxo, and the kernel library that packages validation
for external use. Mempool acceptance *policy* is its own category
(mempool); a change is validation when it touches what is valid, how
chainstate is maintained, or how the node reaches and keeps consensus.

Borderline: a mining or P2P PR that changes when or how blocks are
connected is also validation. A test-only PR is validation if the tests
pin consensus or chainstate behavior.

## What matters here

Consensus correctness above everything: anything that could make the
node accept an invalid block or reject a valid one, or diverge from the
network. Then chainstate integrity: corruption handling, crash safety,
flush and reorg correctness, database invariants. Then resource
exhaustion and adversarial cost: validation-time DoS, memory ceilings
during IBD and reorgs. Then IBD and block-connection performance, which
users feel directly. Then work that makes validation safer to change or
test in isolation, including the kernel project, which is how validation
becomes usable outside bitcoind.

Refactors count when they retire a hazard or unblock one of the above;
renaming and restructuring for their own sake do not.

---
title: Indexes
owner: ryanofsky
labels: ["UTXO Db and Indexes", "Block storage"]
paths: ["src/index", "src/node/blockstorage", "src/txdb", "src/dbwrapper", "src/leveldb"]
keywords: ["txindex", "blockfilterindex", "coinstatsindex", "index sync", "block filter", "BIP157", "BIP158", "leveldb", "dbwrapper", "block storage", "blk*.dat", "rev*.dat", "pruning"]
---

## Covers

The optional indexes (txindex, blockfilterindex, coinstatsindex) and the
base index framework they share, index synchronization and its
performance, the database wrapper and LevelDB integration, block and
undo file storage on disk, and pruning. The "UTXO Db and Indexes" and
"Block storage" labels are a strong prior.

Not indexes: changes to the UTXO set's semantics (validation) or to what
a block filter means (consensus-adjacent; validation).

## What matters here

Data integrity first: an index that silently returns wrong answers or
corrupts on crash is worse than no index. Then correctness under reorgs
and during IBD. Then sync time and resource use, which users of these
indexes feel directly (initial txindex and filter builds take hours).
Then decoupling indexes from node internals so they can be maintained and
tested independently. Then new index types with a stated consumer.

Refactors count when they remove a shared-lock dependency or a
correctness hazard; moving code around does not.

---
title: Indexes
owner: ryanofsky
labels: []
paths: ["src/index", "test/functional/feature_txindex", "test/functional/feature_index", "test/functional/rpc_blockfilter", "test/functional/rpc_txoutproof", "test/functional/feature_coinstatsindex", "test/functional/p2p_blockfilters"]
keywords: ["txindex", "blockfilterindex", "coinstatsindex", "block filter index", "BIP157", "BIP158", "index sync", "BaseIndex", "getblockfilter", "gettxoutsetinfo", "src/index"]
---

## Covers

The optional indexes under `src/index/`: txindex, blockfilterindex
(BIP 157/158 filters), coinstatsindex, and the base index framework they
share (BaseIndex, index synchronization and its performance, index
locking and threading). Plus the RPCs and tests that exist only for
these indexes.

Not indexes: the mandatory structures the node cannot run without. The
UTXO database and coins cache (`src/txdb`, `src/coins`), the block
index and block tree database, block and undo file storage
(`src/node/blockstorage`), pruning, and the database wrapper
(`src/dbwrapper`, LevelDB) are all validation, whatever their names
suggest. The maintainers' "UTXO Db and Indexes" label covers both
groups, so it is not evidence of membership here on its own; the
"Block storage" label is validation.

## What matters here

Data integrity first: an optional index that silently returns wrong
answers or corrupts on crash is worse than no index, and BIP 157
filters are served to light clients. Then correctness under reorgs and
during initial sync. Then sync time and resource use, which users of
these indexes feel directly (initial txindex and filter builds take
hours). Then decoupling the index framework from node internals so
indexes can be maintained and tested independently. Then new index
types with a stated consumer.

Refactors count when they remove a shared-lock dependency or a
correctness hazard; moving code around does not.

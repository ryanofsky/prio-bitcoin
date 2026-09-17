---
title: Validation
owner: ryanofsky
labels: ["Validation", "Consensus", "Block storage", "UTXO Db and Indexes"]
paths: ["src/validation", "src/consensus", "src/node/chainstate", "src/coins", "src/txdb", "src/dbwrapper", "src/chain", "src/script/interpreter", "src/primitives", "src/node/blockstorage", "src/node/utxo_snapshot", "src/flatfile", "src/undo"]
keywords: ["consensus", "chainstate", "reorg", "IBD", "assumeutxo", "block validity", "coins cache", "utxo set", "coins db", "block index", "block tree", "blockstorage", "blk*.dat", "rev*.dat", "pruning", "dbwrapper", "leveldb", "flush", "ConnectBlock", "ActivateBestChain"]
---

## Covers

Changes that substantively alter validation code: block and transaction
validity rules and their implementation, chainstate and block-index
management, the UTXO set and its cache and database (`src/coins`,
`src/txdb`), the block tree database, block and undo file storage and
pruning (`src/node/blockstorage`), the database wrapper and LevelDB
(`src/dbwrapper`), reorg handling, initial block download and
assumeutxo, and the tests that pin this behavior. These mandatory
structures are validation even though some carry "index" or "db" in
their names; the optional indexes under `src/index/` are the separate
`indexes` category. "Substantively" means the change alters what the
node accepts, how chainstate is maintained, how validation performs, or
how a validation invariant is enforced, and a reviewer needs to
understand validation logic to review it.

Not validation:

- PRs whose primary subject is the kernel library API (category
  `kernel`), an optional index under `src/index/` (`indexes`), block
  template construction
  (`mining`), or mempool policy (`mempool`). Those belong there even when
  they touch files under `src/validation`.
- Logging, naming, and structural refactors that pass through validation
  files without changing validation behavior. If such a PR does change
  user-visible behavior of validation (what gets logged when a block is
  rejected, for example), it is validation.

A PR that is primarily a kernel or index change and *also* substantively
changes validation logic is a red flag: it probably needs splitting so
the validation part can get focused review. Say so in the rationale.

The maintainers' `Validation`, `Consensus`, and `Block storage` labels
are a strong prior for membership; "UTXO Db and Indexes" is a prior
when the PR touches the coins database rather than `src/index/`.

## What matters here

Consensus correctness above everything: anything that could make the
node accept an invalid block or reject a valid one, or diverge from the
network. Then chainstate integrity: corruption handling, crash safety,
flush and reorg correctness, database invariants. Then resource
exhaustion and adversarial cost: validation-time DoS, memory ceilings
during IBD and reorgs. Then IBD and block-connection performance, which
users feel directly. Then work that makes validation safer to change or
test in isolation.

Proposed soft forks (new opcodes, new consensus rules) are validation
PRs. Their importance here is the importance of reaching a decision on
them and of the code being correct if activated, not a judgment on
whether the fork should happen.

Refactors count when they retire a hazard or unblock one of the above;
renaming and restructuring for their own sake do not.

---
title: Wallet
owner: ryanofsky
labels: ["Wallet", "Descriptors", "PSBT"]
paths: ["src/wallet", "src/qt/wallet", "src/psbt", "src/script/descriptor", "test/functional/wallet_", "test/functional/rpc_psbt"]
keywords: ["wallet", "descriptor", "psbt", "coin selection", "migration", "sqlite", "bdb", "legacy wallet", "keypool", "watchonly", "fee estimation"]
---

## Covers

The bitcoind wallet: key and descriptor management, transaction creation
and coin selection, PSBT handling, wallet database (SQLite, and the
legacy BDB migration path), backup and recovery, rescanning, wallet RPCs,
and wallet-facing pieces of the GUI. Fee estimation is wallet when the
change is about how the wallet uses it.

Borderline: a descriptor or PSBT change that affects only `bitcoin-tx` or
RPC without wallet code is rpc, not wallet. An `interfaces::Wallet`
change is both wallet and ipc.

## What matters here

Fund safety first: anything that could lose keys, double-spend
unintentionally, create an unspendable output, or corrupt the wallet
database. Then backup, recovery, and migration correctness, including the
legacy-to-descriptor migration path that every remaining legacy user
must cross. Then privacy of transaction creation (address reuse, change
detection, fingerprinting). Then user-visible reliability: hangs, slow
rescans, confusing failures, wrong balances. Then features users have
asked for, with evidence they have asked.

The rubric does not ask whether Bitcoin Core should have a wallet. It
asks, given that it does, what a wallet user needs most.

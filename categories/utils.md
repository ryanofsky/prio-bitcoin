---
title: Utilities (logging, arguments, libraries)
owner: ryanofsky
labels: ["Utils/log/libs", "Resource usage"]
paths: ["src/util", "src/common", "src/logging", "src/init", "src/init.cpp", "src/random", "src/crypto", "src/secp256k1", "src/leveldb", "src/minisketch", "src/univalue", "src/support", "src/sync", "src/threadsafety", "src/tinyformat", "src/serialize", "src/streams", "src/span"]
keywords: ["logging", "LogPrintf", "LogInfo", "ArgsManager", "settings", "bitcoin.conf", "-debug", "init", "shutdown", "util::", "Result", "serialize", "random", "crypto", "sha256", "subtree", "secp256k1", "leveldb", "minisketch", "univalue", "thread", "lock", "sync"]
---

## Covers

Shared infrastructure used across the node: logging, argument and
settings handling, startup and shutdown sequencing, error and result
types, serialization, randomness and cryptographic primitives, threading
and locking utilities, and the vendored subtrees (secp256k1, leveldb,
minisketch, univalue, crc32c). The Utils/log/libs label is a strong
prior.

Not utils: a logging or settings change whose point is one area's
behavior (that area); the kernel API (kernel).

## What matters here

Unlike most categories, internal improvements are the subject here, so
judge them on their own terms. Correctness and safety of primitives
first: randomness, cryptography, serialization, locking, and shutdown
behavior are where subtle bugs become node-wide problems. Then
subtree updates that carry security or correctness fixes. Then
user-facing behavior of configuration and logging: confusing options,
lost log lines, startup failures. Then reductions in a burden every
other area carries: an error-handling pattern that simplifies many call
sites, a logging API that makes categories consistent. Then cosmetic
consistency.

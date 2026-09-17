---
title: Kernel (libbitcoinkernel)
owner: ryanofsky
labels: ["Kernel"]
paths: ["src/kernel", "src/bitcoin-chainstate", "src/test/kernel", "doc/design/libbitcoinkernel"]
keywords: ["kernel", "libbitcoinkernel", "bitcoin-chainstate", "btck_", "kernel API", "kernel library"]
---

## Covers

The libbitcoinkernel project: the C and C++ kernel API, its headers and
bindings, the boundary between the kernel and the rest of the node
(notifications, logging callbacks, error reporting, context and options
objects), the `bitcoin-chainstate` example, kernel tests, and refactors
whose stated purpose is to make validation usable as a library. The
Kernel label is a strong prior.

A kernel PR that also substantively changes validation logic is both
kernel and validation, and probably needs splitting; say so.

Not kernel: changes inside validation that happen to compile into the
kernel library but do not touch its API or its boundary.

## What matters here

Whether external users can build on the library: API completeness for
the stated use cases (validating blocks and transactions, reading
chainstate, receiving notifications), API stability and versioning,
correctness at the boundary (error propagation, thread safety, object
lifetimes), and platform coverage. Then removing node dependencies from
kernel code, which is the project's core work. Then documentation and
examples that determine whether anyone outside the project can use it.

Renames and cosmetic API polish without a consumer asking for them are
P3 or below.

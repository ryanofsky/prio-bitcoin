---
title: IPC / multiprocess
owner: ryanofsky
labels: ["IPC"]
paths: ["src/ipc", "src/interfaces", "src/init/bitcoin-node", "src/init/bitcoin-gui", "src/init/bitcoin-wallet", "src/bitcoin.cpp", "src/ipc/libmultiprocess", "test/functional/interface_ipc"]
keywords: ["ipc", "multiprocess", "capnp", "capnproto", "libmultiprocess", "bitcoin-node", "bitcoin-gui", "bitcoin-wallet", "-ipcbind", "-ipcconnect", "interfaces::"]
---

## Covers

The process-separation project and everything that serves it: the
`interfaces::` abstraction layer between node, wallet, and GUI, the Cap'n
Proto interface definitions and generated-code machinery, the
libmultiprocess subtree, the `bitcoin-node` / `bitcoin-gui` /
`bitcoin-wallet` executables and the `bitcoin` wrapper, IPC process
management (spawning, connecting, disconnect handling), and the tests and
build glue for all of it. The IPC label is a strong prior.

Not ipc: PRs whose subject is what the mining interface exposes or how
templates are built (category `mining`), even though they travel over
IPC. A mining PR is ipc only if it changes IPC infrastructure itself
(serialization, connection handling, the capnp toolchain). Likewise a
wallet or GUI PR that adds a method to `interfaces::Wallet` is wallet
first; it is ipc only if the interface mechanics are the point.

A general-utility PR (a result type, a logging helper) that the
multiprocess stack happens to be based on is not ipc.

## What matters here

Anything that lets external software use the node over IPC reliably: the
stability and completeness of the mining interface and its consumers,
crash and disconnect handling, correctness of serialization across the
process boundary, and platform coverage (the IPC binaries building and
passing tests on every supported platform). Then progress on running the
wallet and GUI as separate processes, which is the project's stated goal.
Then reductions in the maintenance burden of the interface layer:
generated code, build integration, the libmultiprocess subtree sync.

Interface cleanups without a consumer waiting on them are P3 or below.

---
title: IPC / multiprocess
owner: ryanofsky
labels: ["IPC", "Mining"]
paths: ["src/ipc", "src/interfaces", "src/init/bitcoin-node", "src/init/bitcoin-gui", "src/init/bitcoin-wallet", "src/bitcoin.cpp", "src/ipc/libmultiprocess", "test/functional/interface_ipc"]
keywords: ["ipc", "multiprocess", "capnp", "capnproto", "libmultiprocess", "bitcoin-node", "bitcoin-gui", "bitcoin-wallet", "-ipcbind", "-ipcconnect", "interfaces::", "mining interface", "stratum"]
---

## Covers

The process-separation project and everything that serves it: the
`interfaces::` abstraction layer between node, wallet, and GUI, the Cap'n
Proto interface definitions, the libmultiprocess subtree, the
`bitcoin-node` / `bitcoin-gui` / `bitcoin-wallet` executables and the
`bitcoin` wrapper, the IPC mining interface used by external block
template consumers, and the tests and build glue for all of it.

Borderline: a wallet or GUI PR that changes an `interfaces::` method or a
`.capnp` file is also ipc, usually low in this category unless the
interface change is the point. A mining PR that changes what the IPC
mining interface exposes is ipc.

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

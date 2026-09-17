---
title: Mempool and policy
owner: ryanofsky
labels: ["Mempool", "TX fees and policy"]
paths: ["src/txmempool", "src/policy", "src/node/mempool_", "src/kernel/mempool_", "src/validation.cpp", "test/functional/mempool_", "test/functional/feature_rbf", "test/functional/p2p_package"]
keywords: ["mempool", "policy", "RBF", "replace-by-fee", "package relay", "package", "TRUC", "v3", "cluster mempool", "fee estimation", "minfee", "dust", "standardness", "ephemeral", "CPFP", "ancestor", "descendant", "eviction"]
---

## Covers

Which unconfirmed transactions the node accepts, keeps, and relays:
standardness and policy rules, replacement rules, package acceptance
and relay, mempool data structures and limits, eviction, fee
estimation, and the cluster mempool project. The Mempool and TX fees
and policy labels are a strong prior.

Not mempool: consensus validity (validation); block template
construction (mining); the p2p messages that carry transactions (p2p).

## What matters here

Denial-of-service and pinning resistance first: policy is the node's
defense against transactions designed to waste resources or to block
legitimate replacements, and second-layer protocols depend on it. Then
correctness of acceptance and replacement rules against their stated
specifications, since wallets and Lightning implementations build on
them. Then progress on the cluster mempool project and the improvements
it unblocks. Then fee estimation accuracy, which every wallet user
feels. Then memory and CPU behavior under load.

Policy changes with a written rationale and downstream demand rank
above local tidy-ups.

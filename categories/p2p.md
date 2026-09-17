---
title: P2P
owner: ryanofsky
labels: ["P2P", "Private Broadcast"]
paths: ["src/net", "src/net_processing", "src/netbase", "src/netaddress", "src/protocol", "src/addrman", "src/banman", "src/headerssync", "src/txorphanage", "src/txrequest", "src/node/txdownloadman", "src/i2p", "src/torcontrol", "test/functional/p2p_"]
keywords: ["p2p", "peer", "addrman", "eclipse", "relay", "inv", "getdata", "compact block", "BIP152", "BIP324", "v2 transport", "tor", "i2p", "cjdns", "orphan", "headers sync", "DoS", "ban", "disconnect", "private broadcast"]
---

## Covers

Everything between this node and other nodes: connection management and
peer selection, address management, the message protocol and its
transport (including the encrypted v2 transport), block and transaction
relay including compact blocks, headers sync, transaction request and
orphan handling, network-level DoS protections, and the Tor, I2P, and
CJDNS integrations. The P2P and Private Broadcast labels are a strong
prior.

Not p2p: what the node does with a block or transaction once received
(validation, mempool); RPCs that merely report peer state (rpc).

## What matters here

Resistance to attack first: eclipse and partition resistance, DoS
resistance in message handling and resource accounting, and privacy of
transaction origin. Then relay correctness and liveness: blocks and
transactions propagate reliably and quickly, and nothing gets stuck.
Then interoperability with the rest of the network and with new
protocol features (BIPs) that other software depends on. Then bandwidth
and resource use, which node operators feel. Then connectivity across
network types and platforms.

Protocol changes with a specification and other implementations
waiting rank higher than local optimizations. Refactors count when they
retire a known hazard in message handling.

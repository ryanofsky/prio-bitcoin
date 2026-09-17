---
title: RPC / REST / ZMQ
owner: ryanofsky
labels: ["RPC/REST/ZMQ"]
paths: ["src/rpc", "src/rest.cpp", "src/zmq", "src/httpserver", "src/httprpc", "src/bitcoin-cli", "test/functional/rpc_", "test/functional/interface_rest", "test/functional/interface_zmq"]
keywords: ["rpc", "RPCHelpMan", "bitcoin-cli", "REST", "zmq", "notification", "json", "getblock", "getrawtransaction", "http server", "auth cookie", "-rpc"]
---

## Covers

The node's programmatic interfaces: JSON-RPC methods and their help and
argument handling, the HTTP server and authentication, `bitcoin-cli`,
the REST interface, and ZMQ notifications. Wallet RPCs are wallet first
and rpc second unless the change is to the RPC machinery itself. The
RPC/REST/ZMQ label is a strong prior.

Not rpc: the behavior an RPC merely exposes (that belongs to its area).

## What matters here

Compatibility first: changes that break or silently alter what existing
callers get back affect every application built on the node, so
correctness of returned data and the discipline around deprecations
matter most. Then security of the interface: authentication, exposure
of sensitive data, resource exhaustion through the HTTP server. Then
gaps that force applications into workarounds: missing fields or
methods that downstream software has asked for, with evidence they
asked. Then performance of hot methods that block explorers and
indexers call constantly. Then consistency and documentation of the
interface.

New methods without an external consumer asking rank low.

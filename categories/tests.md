---
title: Test infrastructure
owner: ryanofsky
labels: ["Tests", "Fuzzing"]
paths: ["test/functional/test_framework", "test/functional/test_runner.py", "src/test/util", "src/test/fuzz", "test/fuzz", "test/lint", "src/bench", "test/util", "test/sanitizer_suppressions", "src/test/main.cpp", "test/functional/README.md"]
keywords: ["test framework", "test_runner", "fuzz", "harness", "libfuzzer", "sanitizer", "flaky", "intermittent", "bench", "lint", "test coverage", "corpus", "seed", "BOOST_", "unit test infrastructure"]
---

## Covers

The machinery of testing rather than tests of a particular area: the
functional test framework and runner, unit test utilities, the fuzzing
harnesses and corpora, benchmarks, linters, sanitizer configuration,
and fixes for flaky tests whose cause is in the framework. A test that
pins the behavior of one area (a wallet migration test, a p2p relay
test) belongs to that area, not here. The Tests and Fuzzing labels are
a prior, but a labeled PR whose tests are about one area goes to that
area instead.

## What matters here

Signal first: fixes for flaky or misleading tests, since a red CI that
nobody trusts hides real failures. Then coverage of high-risk code paths
that the fuzzers or functional tests do not reach, especially
consensus, mempool policy, and p2p message handling. Then framework
capabilities that unblock tests other areas need. Then test speed, which
every contributor pays for on every run. Then cleanliness of the test
code.

Adding tests for their own sake ranks low; adding a test that catches a
realistic regression ranks high.

---
title: Documentation
owner: ryanofsky
labels: ["Docs"]
paths: ["doc/", "README.md", "CONTRIBUTING.md", "src/rpc/", "doc/release-notes", "doc/policy", "doc/design"]
keywords: ["doc", "documentation", "release notes", "README", "typo", "comment", "design doc", "developer notes", "help text"]
---

## Covers

Documentation as the primary change: developer notes, design documents,
build and usage docs, release notes, RPC help text when the change is
to the text rather than the interface, and code comments when a PR
consists mainly of them. The Docs label is a strong prior.

Not docs: a code change that also updates its docs (that area).

## What matters here

Wrong documentation first: text that would lead a user or developer to
do the wrong thing, especially around security, backups, and
configuration. Then missing documentation for something users hit often
or that a design decision depends on (a design doc that unblocks a
project counts as leverage). Then release notes completeness. Then
clarity improvements to frequently read pages. Then typo and style
fixes, which are P4 unless they fix a meaning.

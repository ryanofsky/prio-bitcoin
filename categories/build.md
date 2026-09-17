---
title: Build and CI
owner: ryanofsky
labels: ["Build system", "Windows", "macOS", "DrahtBot Guix build requested"]
paths: ["CMakeLists.txt", "cmake/", "depends/", "ci/", "contrib/guix", "contrib/devtools", ".github/", "contrib/verify", "build-aux", "doc/build", "contrib/macdeploy", "contrib/windeploy"]
keywords: ["cmake", "depends", "guix", "ci", "reproducible", "cross-compile", "mingw", "msvc", "clang", "gcc", "libc++", "sanitizer", "-Werror", "vcpkg", "release process", "qt build", "boost", "libevent", "sqlite", "capnp build"]
---

## Covers

How the project is built, tested, and released: the CMake build system,
the depends system and its packages, Guix reproducible builds, CI
configuration and scripts, compiler and platform support, and the
tooling under contrib used for releases and development. Platform
labels (Windows, macOS) point here when the change is about building or
running on that platform rather than about a feature. The Build system
label is a strong prior.

Not build: source changes that happen to fix a compiler warning as a
side effect (they belong to their area).

## What matters here

Release integrity first: reproducibility of Guix builds, correctness of
dependency pinning and verification, and anything that could ship a
wrong binary. Then supported-platform breakage: a platform that fails
to build or run blocks users on it. Then CI reliability: flaky or
misleading jobs waste every contributor's time and hide real failures.
Then dependency transitions with deadlines (compiler or library minimum
versions, deprecations upstream). Then build time and contributor
friction.

Cosmetic CMake cleanups rank low unless they remove a recurring
breakage.

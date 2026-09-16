# prio-bitcoin

Categories, definitions of importance, and human feedback for the Bitcoin
Core instance of [prio](https://github.com/ryanofsky/prio), a
category-scoped map of which open PRs are worth review time.

This repo is about the *contents* of the site: which categories exist,
what each considers important, and corrections to the machine's
judgments. Discussion about how the site works belongs in the engine
repo.

The site is a personal, opinionated tool. Its rankings are model output
against the files here, labeled as such, with the rationale and inputs
exposed. It is not a Bitcoin Core project process and does not claim to
be.

## Layout

```
project.toml            repos covered, bots, thresholds
categories/<name>.md    one file per category: what it covers, what matters in it
feedback/prs/<n>/       one file per feedback entry about a PR
feedback/categories/    one file per feedback entry about a category's ranking
```

Shared definitions (what makes a PR important, the P1–P4 bands,
Reviewability, Agreement) live in the engine repo under `definitions/`.

## Adding or changing a category

Open a pull request that adds or edits `categories/<name>.md`. The file
has front matter and two sections:

```markdown
---
title: Validation
owner: ryanofsky
labels: ["Validation", "Consensus"]        # GitHub labels that suggest membership
paths: ["src/validation", "src/consensus"] # path prefixes that suggest membership
keywords: ["reorg", "chainstate"]          # words in title/body that suggest membership
---

## Covers
What is in this category, and the borderline cases.

## What matters here
What "impact" means in this area, concretely.
```

The hints only decide which categories the model is asked about for a
PR; membership itself is the model's call against the "Covers" text.
Membership is inclusive: a PR belongs to every category whose area it
touches, and may be important in one and marginal in another.

## Giving feedback

Open a pull request adding a file under `feedback/`, or (once the site
has login) use the form on a PR row. Each entry is one file:

```markdown
---
author: <github login>
author_id: <numeric id>
date: 2026-09-16T14:02:11Z
pr: 30342
category: validation        # optional for facts, required for opinions
kind: fact                  # fact | opinion | retract
head: 687074dd              # head SHA the entry refers to (optional)
via: git                    # git | web
---
The concern about X was resolved in the August push; what remains is a
naming disagreement.
```

Facts (wrong category, missing dependency, resolved concern, wrong
summary) are fed to the model when it next assesses that PR. Opinions
("this is P1 because ...") are fed to the ranking pass and shown verbatim
next to the model's result, never averaged into it. Every entry is
attributed and stays in git history.

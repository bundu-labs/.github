# Bundu Labs — org-wide defaults

> The community-health files, lint configs and branch-protection rulesets
> every `bundu-labs` repository inherits.

[![Lint](https://github.com/bundu-labs/.github/actions/workflows/lint.yml/badge.svg)](https://github.com/bundu-labs/.github/actions/workflows/lint.yml)
[![Org profile](https://img.shields.io/badge/org-bundu--labs-24292e?logo=github&logoColor=white)](https://github.com/bundu-labs)
[![Doctrine](https://img.shields.io/badge/doctrine-nyuchi%2F.github-blue)](https://github.com/nyuchi/.github)

**Org:** [github.com/bundu-labs](https://github.com/bundu-labs) | **Foundation:** [bundu.family](https://bundu.family) | **Docs:** [docs.bundu.org](https://docs.bundu.org) | **Engineering doctrine:** [`nyuchi/.github`](https://github.com/nyuchi/.github)

---

This repository holds the org-wide defaults for the
[`bundu-labs`](https://github.com/bundu-labs) GitHub organisation — the
development arm of the [Bundu Foundation](https://bundu.family).

Every repository under `bundu-labs` inherits the community-health files
in this repo unless that repository ships its own. The
[engineering doctrine](https://github.com/nyuchi/.github) — Conventional
Commits, signed commits, DCO, reusable CI workflows — is canonical at
[`nyuchi/.github`](https://github.com/nyuchi/.github) and applies here
too. Documents in this repo defer to the Nyuchi org-wide canon where
appropriate.

## What's in here

| Path                                                                                               | Purpose                                                                         |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `README.md`                                                                                        | This file.                                                                      |
| `profile/README.md`                                                                                | Landing page rendered at <https://github.com/bundu-labs>.                       |
| `SECURITY.md`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SUPPORT.md`, `AGENTS.md`, `GOVERNANCE.md` | Org-wide community-health defaults.                                             |
| `.editorconfig`, `.prettierrc`, `.prettierignore`, `.markdownlint.jsonc`, `.yamllint.yaml`         | Lint / formatter starting configs. Each consumer repo should ship its own copy. |
| `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE/*`                                     | Default PR + issue forms.                                                       |
| `.github/CODEOWNERS`                                                                               | Default reviewers for changes here.                                             |
| `.github/dependabot.yml`, `.github/dependabot.example.yml`                                         | Dependabot for _this_ repo, plus a starting template for consumer repos.        |
| `.github/workflows/*.yml`                                                                          | CI for _this_ repo (lint, PR-title, stale).                                     |
| `github-rulesets/*.json`                                                                           | Branch-protection rulesets for downstream repos to apply via `gh api`.          |

## Reusable CI workflows

Reusable workflows live in
[`nyuchi/.github/.github/workflows/`](https://github.com/nyuchi/.github/tree/main/.github/workflows).
Reference them from a consumer repo's workflow:

```yaml
jobs:
  lint:
    uses: nyuchi/.github/.github/workflows/reusable-lint.yml@main
```

The reusable set covers PR-title lint, lint, CodeQL, dependency review,
SBOM, stale, and release.

## Branch protection rulesets

`github-rulesets/main-branch-protection.json` is the standard
per-repository main-branch ruleset (linear history, signed commits,
PR review, required status checks). Apply to any `bundu-labs` repo
via:

```sh
gh api repos/bundu-labs/<repo>/rulesets \
  -X POST \
  --input github-rulesets/main-branch-protection.json
```

## Engineering doctrine

For the canonical engineering working agreement, governance, and
contribution rules, see
[`nyuchi/.github`](https://github.com/nyuchi/.github):

- [`CONTRIBUTING.md`](https://github.com/nyuchi/.github/blob/main/CONTRIBUTING.md)
- [`AGENTS.md`](https://github.com/nyuchi/.github/blob/main/AGENTS.md)
- [`GOVERNANCE.md`](https://github.com/nyuchi/.github/blob/main/GOVERNANCE.md)
  → references the `NA-01 Constitution`, `NA-02 Open Source`, and
  `NA-03 Engineering Working Agreement` documents.

Bundu Labs is the foundation's dev arm; its standards mirror Nyuchi's
unless an explicit Bundu-specific exception is documented.

## The README standard

Every repository in the estate — `bundu-labs` included — opens the same way:
title, one-line purpose, badges, an at-a-glance line, what it is, then
licence and governance. The derived standard is `README-STANDARD.md` in
[`nyuchi/.github`](https://github.com/nyuchi/.github), landing via
[PR #62](https://github.com/nyuchi/.github/pull/62). Read it before writing
or rewriting a README here.

Two rules from it are worth repeating, because they are the ones that get
broken:

- **A README that is wrong is worse than a README that is thin.** Consistency
  means the same shape, never the same prose. If you cannot honestly describe
  a repo, write one true sentence and stop.
- **Curl every URL and badge before you commit it.** A dead badge is a broken
  promise on the most public page a project has.

## Licence and governance

The [Bundu Foundation](https://bundu.family) (Zimbabwean Company Limited by
Guarantee) is the governance body for this organisation;
[Nyuchi](https://nyuchi.com) is the operator. These are org-wide defaults, not
a shipped artefact — each consumer repo carries its own `LICENSE`.

© Bundu Foundation, operated by Nyuchi Africa (Pvt) Ltd.

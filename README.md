# bundu-labs/.github

Org-wide defaults for the [`bundu-labs`](https://github.com/bundu-labs)
GitHub organisation — the development arm of the
[Bundu Foundation](https://bundu.family).

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
| `.github/dependabot.example.yml`                                                                   | Starting template for consumer repos.                                           |
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

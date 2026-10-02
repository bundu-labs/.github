# Bundu Labs — org-wide defaults

> The community-health files, lint configs and branch-protection rulesets
> every `bundu-labs` repository inherits.

[![Org lint](https://github.com/bundu-labs/.github/actions/workflows/org-lint.yml/badge.svg)](https://github.com/bundu-labs/.github/actions/workflows/org-lint.yml)
[![Org profile](https://img.shields.io/badge/org-bundu--labs-24292e?logo=github&logoColor=white)](https://github.com/bundu-labs)
[![Doctrine](https://img.shields.io/badge/doctrine-nyuchi%2F.github-blue)](https://github.com/nyuchi/.github)

**Org:** [github.com/bundu-labs](https://github.com/bundu-labs) | **Foundation:** [bundu.org](https://www.bundu.org) | **Docs:** [docs.bundu.org](https://docs.bundu.org) | **Engineering doctrine:** [`nyuchi/.github`](https://github.com/nyuchi/.github)

---

This repository holds the org-wide defaults for the
[`bundu-labs`](https://github.com/bundu-labs) GitHub organisation — the
enterprise of the [Bundu Foundation](https://www.bundu.org) — and the
canonical [Bundu Order](profile/canonical/BUNDU_ORDER.md).

Every repository under `bundu-labs` inherits the community-health files
in this repo unless that repository ships its own. The
[engineering doctrine](https://github.com/nyuchi/.github) — Conventional
Commits, signed commits, DCO, reusable CI workflows — is canonical at
[`nyuchi/.github`](https://github.com/nyuchi/.github) and applies here
too. Documents in this repo defer to the Nyuchi org-wide canon where
appropriate.

## What's in here

| Path                                                                                                                   | Purpose                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `README.md`                                                                                                            | This file.                                                                                                                             |
| `profile/README.md`                                                                                                    | Landing page rendered at <https://github.com/bundu-labs>.                                                                              |
| `profile/canonical/BUNDU_ORDER.md`                                                                                     | **The Bundu Order v5.0.0** (October 2026), the Founder's text, unedited. Exempt from Prettier and markdownlint.                        |
| `SECURITY.md`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SUPPORT.md`, `AGENTS.md`, `GOVERNANCE.md`                     | Org-wide community-health defaults.                                                                                                    |
| `.editorconfig`, `.prettierrc`, `.prettierignore`, `.markdownlint.jsonc`, `.markdownlint-cli2.jsonc`, `.yamllint.yaml` | Lint / formatter configs for _this_ repo. Consumer repos need none: the shared lint falls back to `nyuchi/.github`'s canonical copies. |
| `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE/*`                                                         | Default PR + issue forms.                                                                                                              |
| `.github/CODEOWNERS`                                                                                                   | Default reviewers for changes here.                                                                                                    |
| `.github/dependabot.yml`, `.github/dependabot.example.yml`                                                             | Dependabot for _this_ repo, plus a starting template for consumer repos.                                                               |
| `.github/workflows/*.yml`                                                                                              | `org-lint.yml` is the org-required lint for every `bundu-labs` repo; PR-title and stale run for _this_ repo.                           |
| `workflow-templates/lint.yml`                                                                                          | The lint caller offered under **Actions → New workflow**. Not needed: lint is already org-required.                                    |
| `github-rulesets/*.json`                                                                                               | The org ruleset (`org-wide-main-protection`) as applied, and a `release-tag-protection` template (not applied).                        |

## Reusable CI workflows

Reusable workflows live in
[`nyuchi/.github/.github/workflows/`](https://github.com/nyuchi/.github/tree/main/.github/workflows).
Reference them from a consumer repo's workflow, for example:

```yaml
jobs:
  codeql:
    uses: nyuchi/.github/.github/workflows/reusable-codeql.yml@main
```

The reusable set covers PR-title lint, lint, CodeQL, dependency review,
SBOM, stale, and release.

**Lint needs no caller.** The org ruleset's "Require workflows to pass"
rule runs [`.github/workflows/org-lint.yml`](.github/workflows/org-lint.yml)
on every pull request in every `bundu-labs` repository. It calls
`nyuchi/.github`'s `reusable-lint.yml` and publishes the five required
checks (`lint / actionlint`, `lint / JSON validity`, `lint / prettier`,
`lint / markdownlint`, `lint / yamllint`). A repository needs no
`lint.yml` and no lint config files: its own `.prettierrc`,
`.prettierignore`, `.markdownlint.jsonc` or `.yamllint.yaml` win where
present, and the canonical copies in `nyuchi/.github` apply where not.

## Branch protection rulesets

Two rulesets protect the default branch of every `bundu-labs` repository
except `sandbox-*` and `archive-*`:

- **`enterprise-main-protection`**, set on the `bundu-labs` enterprise and
  **active** in every org of the enterprise: pull request required with
  **0** approvals, linear history, no force pushes, no deletion.
- **`org-wide-main-protection`**, this org's ruleset
  ([`github-rulesets/org-wide-main-protection.json`](github-rulesets/org-wide-main-protection.json)):
  the same floor, squash or rebase merges, resolved review threads, the
  five lint status checks (strict), and the required `org-lint.yml`
  workflow.

Organisation admins can bypass both. There is no per-repository copy of
these rules and no classic branch protection; a repository may add one
`repo-ci` ruleset holding only its own CI checks. The full standard is in
[`nyuchi/.github` → `ORG_SETTINGS.md`](https://github.com/nyuchi/.github/blob/main/ORG_SETTINGS.md).
To update the org ruleset, PUT the JSON to its id:

```sh
gh api orgs/bundu-labs/rulesets --jq '.[] | [.id, .name] | @tsv'
gh api --method PUT /orgs/bundu-labs/rulesets/<id> \
  --input github-rulesets/org-wide-main-protection.json
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

Bundu Labs follows Nyuchi's engineering standards unless an explicit
Bundu-specific exception is documented.

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

The [Bundu Foundation](https://www.bundu.org) (a Zimbabwe company limited by
guarantee; incorporation pending) is the governance body for this organisation;
[Nyuchi](https://nyuchi.com) is the operator. These are org-wide defaults, not
a shipped artefact — each consumer repo carries its own `LICENSE`.

© Bundu Foundation, operated by Nyuchi Africa (Pvt) Ltd.

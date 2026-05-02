# Governance

`bundu-labs` is the development arm of the
[Bundu Foundation](https://bundu.family). The Foundation's governance
posture follows the Nyuchi Africa working agreement, published at:

| Document | Contents |
| -------- | -------- |
| [NA-01 — Constitution](https://github.com/nyuchi/.github/blob/main/profile/governance/NA-01_CONSTITUTION.md) | Legal identity, purpose, decision rights, divisional structure, IP ownership, amendment process. |
| [NA-02 — Open Source & Contribution Governance](https://github.com/nyuchi/.github/blob/main/profile/governance/NA-02_OPEN_SOURCE.md) | Licensing posture, sovereignty fallbacks, contribution principles, CLA, community standards. |
| [NA-03 — Engineering Working Agreement](https://github.com/nyuchi/.github/blob/main/profile/governance/NA-03_ENGINEERING.md) | Frontier defaults, locked architectural commitments, merge-blocker reference. |

Day-to-day mechanics — Conventional Commits, signed commits, DCO, CI
requirements — live in [`CONTRIBUTING.md`](./CONTRIBUTING.md) and
[`AGENTS.md`](./AGENTS.md).

GitHub-level settings (branch protection rulesets, required reviewers,
secret scanning, etc.) follow
[`nyuchi/.github → ORG_SETTINGS.md`](https://github.com/nyuchi/.github/blob/main/ORG_SETTINGS.md).
The
[`github-rulesets/`](./github-rulesets) directory in this repo holds
the JSON for `bundu-labs`-applicable rulesets, ready to apply via
`gh api`.

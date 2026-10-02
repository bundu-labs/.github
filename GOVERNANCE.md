# Governance

`bundu-labs` is the enterprise of the
[Bundu Foundation](https://www.bundu.org), which owns the IP of the
ecosystem and governs it.

## The canonical documents

| Document                                                                                                        | Owner            | What it is                                                                    |
| --------------------------------------------------------------------------------------------------------------- | ---------------- | ----------------------------------------------------------------------------- |
| [The Bundu Order](profile/canonical/BUNDU_ORDER.md)                                                             | Bundu Foundation | The mathematical architecture of the ecosystem and the Locked Count Register. |
| [The Nyuchi Architecture](https://github.com/nyuchi/.github/blob/main/profile/canonical/NYUCHI_ARCHITECTURE.md) | Nyuchi Africa    | The canonical technical architecture. Wins over every other document.         |
| [The Mukoko Manifesto](https://github.com/mukoko-dev/.github/blob/main/profile/canonical/MUKOKO_MANIFESTO.md)   | Mukoko           | The platform philosophy and the Seven Covenants.                              |

All three are version 5.0.0 (October 2026) and are changed only by the
Founder. The counts in the Bundu Order's Locked Count Register change
only when he initiates the revision.

## Operating governance

Day-to-day governance follows the Nyuchi Africa working agreement,
published at:

| Document                                                                                                                             | Contents                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| [NA-01 — Constitution](https://github.com/nyuchi/.github/blob/main/profile/governance/NA-01_CONSTITUTION.md)                         | Legal identity, purpose, decision rights, divisional structure, IP ownership, amendment process. |
| [NA-02 — Open Source & Contribution Governance](https://github.com/nyuchi/.github/blob/main/profile/governance/NA-02_OPEN_SOURCE.md) | Licensing posture, sovereignty fallbacks, contribution principles, CLA, community standards.     |
| [NA-03 — Engineering Working Agreement](https://github.com/nyuchi/.github/blob/main/profile/governance/NA-03_ENGINEERING.md)         | Frontier defaults, locked architectural commitments, merge-blocker reference.                    |

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

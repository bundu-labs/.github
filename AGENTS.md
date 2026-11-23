# AGENTS.md

**Rules for AI-assisted contributions to `bundu-labs` repositories.**

This file is **org-wide** for the
[`bundu-labs`](https://github.com/bundu-labs) GitHub org. It applies
to any AI coding agent — Claude Code, Cursor, GitHub Copilot, Aider,
Codex CLI, etc. — making changes in any repo under `bundu-labs`.

The canonical AI-agent doctrine is at
[`nyuchi/.github → AGENTS.md`](https://github.com/nyuchi/.github/blob/main/AGENTS.md).
This file mirrors the relevant rules. Repo-level `AGENTS.md` (or a
tool-specific `CLAUDE.md`) layers on top; repo rules win where they
conflict.

> **Authoritative for agents. Advisory for humans.**

## Mission (owner, 2026-10-24)

Read this first. It applies to every repository in the Bundu ecosystem, and
every decision is judged against the whole platform, not only the repo in
front of you.

**What we are building.** A platform built to compete with the top five
platforms in the world. It is built from Africa, but not as "a product for
Africa". By default it is open data on published open standards, with no
proprietary data structures, so any system can connect to our data,
transformations and services.

**The ecosystem.** Read nyuchi.com, bundu.org, mukoko.com and mzizi.dev, and
their `llms.txt` files.

- **Bundu Foundation** governs the standards and doctrine. Ubuntu is the spec:
  survival, solidarity, compassion, respect, dignity. Personal data stays on
  the user's device or pod, under the user's keys. No surveillance business
  model. The data commons is open.
- **Nyuchi Africa** is the frontier infrastructure (API Platform, Pay, Web
  Services, Weather Stations, Logistics and more), with the console at
  platform.nyuchi.com.
- **Mukoko** is a privacy-first consumer super-app: one identity, one payments
  rail, offline-first sync, and English, Shona and Ndebele at parity. Kweli is
  its trust and verification layer.
- **Mzizi** is the open architecture framework and language, built on Rust.
  Mzizi is the rule: no app drifts from it, and filling a design-system gap
  so an app conforms to Mzizi needs no approval.
- **Four gateways** (nyuchi-api#353), each rebuilt in Rust on the same layout,
  core, origin and edge (nyuchi-api#355):
  - Mzizi API: public.
  - Nyuchi API: B2B, api.nyuchi.com.
  - Mukoko API: consumer.
  - Nyuchi Servers API: internal, no public IP.

**The engineering bar**, for every service and data model:

1. **Open standards by default** (nyuchi-api#369). Never invent a format when
   a published standard exists:
   - schema.org types with JSON-LD; GeoJSON (RFC 7946) for places;
   - ISO 3166 for countries, ISO 4217 for currencies, RFC 3339 for times,
     BCP 47 for languages (`en`, `sn`, `nd`);
   - CloudEvents for events and DCAT for open datasets;
   - OpenAPI 3.1 for every API;
   - RFC 9457 Problem Details for every error;
   - OAuth 2.1 and OIDC, with RFC 9728 protected-resource metadata;
   - W3C Trace Context and OpenTelemetry;
   - IETF RateLimit headers.
2. **Nothing crashes.** A handler panic becomes a 500 and the process keeps
   serving. Requests have timeouts and size limits. Services shut down
   gracefully. `/health` is liveness and `/ready` checks each dependency. The
   version reported is the real release, never hard-coded.
3. **Everything ships to production.** Releases go `staging` → `main` through
   the merge queue. Deploys run on every push to `main`, with no variable
   gates. A missing secret fails loudly, never silently skips.
4. **Never close a conflicting PR.** Resolve the conflict and keep every
   feature.
5. **Think as a data scientist, a software engineer, a psychologist and an
   engagement designer at once.** Every record is linkable across systems by
   one canonical id: WorkOS `externalId` = Mongo entity id = ledger
   `owner_id`. An empty screen loses a user, so design for engagement and
   trust.
6. **Honesty.** Report what is measured, label design as design, and never
   overclaim.

**Dependencies.** Declare first-party packages (`@nyuchi/*`, `@bundu/*`,
`mzizi-*`) and direct dependencies as minimum versions (`>=x.y.z`) with no
upper bound; an old version blocks, the latest never does. Third-party
selectors known to break across majors, and runtime dependencies of
published packages, are capped within their major (`>=x <next-major`).

## Before you touch the code

Agents must read, in order:

1. The repository's `README.md`.
2. The repository's `CONTRIBUTING.md` (or this org's
   [`CONTRIBUTING.md`](./CONTRIBUTING.md) if the repo doesn't ship
   its own).
3. The repository's `CODEOWNERS` file, if present.
4. Any `AGENTS.md` or `CLAUDE.md` at the repo root.
5. The specific file(s) you intend to modify, **in full**, before
   proposing changes.

**Do not propose changes to code you have not read.**

## Commit and PR conventions

All of [`CONTRIBUTING.md`](./CONTRIBUTING.md) applies to agent
contributions without exception. In particular:

- **[Conventional Commits 1.0](https://www.conventionalcommits.org/en/v1.0.0/)**
  on every commit and every PR title.
- **Signed commits** on every commit that will land on `main`
  (GPG or SSH, verified by GitHub).
- **DCO sign-off** on every commit via `git commit -s`. The agent
  must use the **human operator's** identity for the sign-off — the
  human is the contributor of record. Agents must **not** invent or
  use fake `Signed-off-by` trailers.

### Reserved branch-name prefixes for agents

| Prefix     | Agent                                   |
| ---------- | --------------------------------------- |
| `claude/`  | Claude Code (Anthropic)                 |
| `cursor/`  | Cursor background agent                 |
| `copilot/` | GitHub Copilot Workspace / coding agent |

## Local docs and design references

Many `bundu-labs` repos consume **[Mzizi](https://mzizi.dev/)**, the
design system that replaced the Nyuchi Design System (a Bundu
Foundation project, built by Nyuchi), and the engineering doctrine
canonical at
[`nyuchi/.github`](https://github.com/nyuchi/.github). When working
in such a repo:

- The repo's own `docs/` (if present) is the source of truth for
  repo-specific decisions.
- The Nyuchi Design MCP (`design.nyuchi.com/mcp`) is the source of
  truth for design tokens, brand info, components, Ubuntu doctrine.
- Treat AI-agent scratch files (`CLAUDE.md`, `GEMINI.md`,
  `.claude/`, `.cursor/`) as local-only — they are gitignored in
  most repos.

## Verify before you claim done

Run the repo's verification commands (`typecheck`, `lint`, `test`,
`build`) before claiming the work is complete. CI will catch what
you missed, but you should not be surprised by what it catches.

## When in doubt

- Check the repo's docs first.
- Check `nyuchi/.github` for engineering doctrine.
- Check the Nyuchi Design MCP for design / brand questions.
- Ask before introducing a new top-level surface or making changes
  outside the explicit task scope.

## Track big work in GitHub issues

Any substantial build, migration, investigation or multi-step task gets a GitHub
issue in the repo that owns it — before or as work starts — so another session,
agent or person can pick it up.

- The issue holds the goal, the owner's decisions (verbatim where given), the
  plan, acceptance criteria, owner-only steps and links.
- Every PR references its issue (`Refs #n`; `Fixes #n` only when the merge
  completes it).
- Post progress, decisions and a hand-off note (what's done, what's left, branch
  names) as issue comments — at each merge and before a session or agent
  finishes.
- Work spanning repos gets a tracking issue that links the per-repo issues.
- Never put secrets, credential status or exploitable detail in issues on public
  repos.

## Branches, releases and merging

- Work branches off `staging` and PRs land in `staging`. Each merge into
  `staging` is tagged the next patch (`staging-version.yml`); a release to
  `main` tags the next minor. Both use `nyuchi/.github`'s versioning
  policy, pinned by SHA. Never hand-edit a version to a major.
- Branch prefixes: `feat/`, `fix/`, `docs/`, or `claude/` for agent work.
- PR titles are Conventional Commits: lowercase, imperative subject, no
  trailing period (a subject starting with an all-caps word fails).
- Merges into `staging` are squash through the merge queue
  (`gh pr merge <n> --squash --auto`); the squash body keeps every commit
  message (`COMMIT_MESSAGES`). Updating a branch with its base is fine.
- `staging` is promoted to `main` with a **merge commit**, never squash:
  a merge commit keeps `main` at `staging` plus one merge, so the next
  release cannot conflict and nothing diverges.
- The default branch takes releases only: a PR into `main` must come from
  `staging`, a `release/*` branch, or the registry pin bot
  (`bot/registry-pin`). Everything else — features, fixes, Dependabot —
  targets `staging`.
- Anything that reaches `main` outside a release (hotfix, pin bot) is
  forward-ported to `staging` before the next release; the release check
  blocks the release until then (the `forward-ported` label).
- One writer per branch. Land with `gh pr merge <n> --auto`, which joins
  the merge queue; every workflow whose check is required must also
  trigger on `merge_group:`. Treat GitHub 5xx and "merge already in
  progress" as a wait, not a failure.
- Shared workflows are pinned estate-wide, every repo at the same commit:
  `nyuchi/.github/.github/workflows/<workflow>.yml@<40-hex sha>  # vX.Y.Z`
  (two spaces before `#`); Dependabot raises the pin after each release.
  Never `@main`, never a bare SHA without its tag comment.
- Advisory waivers are org-level only (`AUDIT_ALLOW_GHSAS` in
  `nyuchi/.github`), each with a reason and a review date; a repo cannot
  waive its own advisory.

## Checks that gate every pull request

- `org-lint.yml` in this repo is required on every PR in the org.
- The enterprise rulesets also run `nyuchi/.github`'s release version check,
  dependency review and Semgrep on every PR into `staging` and `main`.
- Every workflow whose check is required must also trigger on `merge_group:`.
- Never disable or weaken a check to get green; fix the cause or escalate.

## Dev skills, progress reports and the merge gate

Load the Mzizi **dev skills** before starting work:
`mzizi_get_skills category=dev` on the Mzizi MCP (`mcp.mzizi.dev`), or
`@nyuchi/mzizi-skills` from npm. They are `digital-hygiene` and
`progress-report`.

- **Digital hygiene.** Check free disk before starting, clone only under
  `$TMPDIR`, share build caches, and audit, then delete, your clones once the
  work merges (`digital-hygiene` skill).
- **Clone isolation.** Clone only into a directory unique to you; never touch
  another agent's.
- **Progress reports.** All dev work runs on a 10-minute progress-report loop
  (`progress-report` skill): measured bars, what changed, and a final "Needs
  you:" line. Report ticks never publish, release, merge or deploy without the
  owner's approval.
- **Merge gate.** Merge only when the work is complete, CI is green, it's
  verified at runtime, and `/code-review` has run with findings resolved.

## GitHub environments

Owner decision, 2026-11-23. A repository uses only these environment names,
all lowercase, and there is no `staging`:

| Name         | Used for                                                         |
| ------------ | ---------------------------------------------------------------- |
| `release`    | Tag-triggered publishing of packages and artifacts to registries |
| `production` | Deploys                                                          |
| `publish`    | Publishing docs or pages sites                                   |

- Restrict `release` and `production` to `v*` tags, and to `main` as well
  where the workflow deploys by push or dispatch from `main`. No required
  reviewers: releases are automatic.
- GitHub cannot rename an environment: create the new one, change every
  workflow, merge, then delete the old one. Never delete one whose secrets
  you cannot recreate.
- Environments that Vercel, GitHub Pages, Copilot, Mintlify or another app
  creates (`Production`, `Preview`, `Production – <project>`, `github-pages`,
  `copilot`) are theirs; leave them alone. A name fixed by an outside
  trusted-publisher setting (PyPI's `pypi`) stays as registered.
- nyuchi/.github's `repo-standards.yml` warns on a workflow that names any other environment.

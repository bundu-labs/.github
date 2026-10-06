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

Many `bundu-labs` repos consume the **Nyuchi Design System** and
the engineering doctrine canonical at
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

## Dev skills, progress reports and the merge gate

Load the Mzizi **dev skills** before starting work:
`mzizi_get_skills category=dev` on the Mzizi MCP (`mcp.mzizi.dev`), or
`@nyuchi/mzizi-skills` from npm. They are `digital-hygiene` and
`progress-report`.

- **Digital hygiene.** Check free disk before starting, clone only under
  `$TMPDIR`, share build caches, and audit, then delete, your clones once the
  work merges (`digital-hygiene` skill).
- **Progress reports.** All dev work runs on a 10-minute progress-report loop
  (`progress-report` skill): measured bars, what changed, and a final "Needs
  you:" line. Report ticks never publish, release, merge or deploy without the
  owner's approval.
- **Merge gate.** Merge only when the work is complete, CI is green, it's
  verified at runtime, and `/code-review` has run with findings resolved.

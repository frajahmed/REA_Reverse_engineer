# REA_Reverse_engineer

Reverse engineer anything with agents: an agent skill for the
[REA](https://github.com/morluto/rea) MCP server, packaged for Claude and
other skill-aware agents.

The skill teaches an agent how to investigate shipped software (native
binaries, .NET assemblies, Android APKs, Electron/JavaScript apps, archives
and installers, firmware, network captures and live browser behavior) and
how to build AgentEnv bundles of web applications. Every conclusion is tied
to Evidence IDs and separates observations, inferences and unknowns.

## What's inside

```
skills/
  reverse-engineer-anything/
    SKILL.md              core workflow: prerequisites, connection, routing, evidence
    references/
      routing.md          complete target-to-tool routing list
      native-and-artifacts.md
      javascript-applications.md
      android-applications.md
      runtime-observation.md
      evidence-workflows.md
      connection-and-recovery.md
      environments.md
docs/                     REA guides the skill links to (one per format/tool)
```

## Requirements

The skill is a playbook; the analysis tools come from REA itself:

```bash
npx rea-agents setup
```

Install the engine for your target type separately when you need it, for
example Ghidra + Java for native code, JADX for Android, Binwalk/Unblob for
firmware, or Wireshark `tshark` for packet captures. See
[docs/installation.md](docs/installation.md).

## Install the skill

- **Claude (claude.ai / desktop):** zip the `skills/reverse-engineer-anything`
  folder and upload it in Claude's skills settings.
- **Claude Code:** copy the folder to `~/.claude/skills/` (personal) or
  `.claude/skills/` (per project).
- **Other agents:** copy the folder wherever your agent loads skills from.

## Changes from upstream

Based on `.agents/skills/reverse-engineer-anything` (skill version 53) from
[morluto/rea](https://github.com/morluto/rea).

- **Shorter `SKILL.md`** (about 14 KB instead of 35 KB). The long target routing
  list moved to `references/routing.md`; `SKILL.md` keeps a table of the most
  common routes.
- **New Prerequisites section** that states up front that the REA MCP server
  and the per-format engines must be installed.
- **Self-contained links.** The guides the skill references are copied into
  `docs/`, so links stay working even if upstream changes.
- **Trigger-focused description** in the skill frontmatter.
- The four maintainer-only skills (`rea-analysis-optimization`,
  `rea-ci-tests-audit`, `rea-changelog-update`, `rea-tool-design`) are left out
  because they only work inside the REA source repository.

## License

MIT. Original work © 2026 morluto; see [LICENSE](LICENSE). Only use REA on
software you own or are authorized to analyze.

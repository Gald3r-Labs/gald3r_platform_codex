# gald3r Readiness Report — OpenAI Codex

> An honest accounting of how much of the gald3r framework installs natively on this
> platform, what degrades to an approximation, and what has no native home yet.
> Generated from a live documentation crawl on 2026-06-02.

**Overall readiness: ✅ Full.** OpenAI Codex (CLI / IDE / app) exposes a native extension
point for every gald3r primitive. Commands, rules, agents, skills, and hooks all map 1:1
onto first-class mechanisms — and the skill format is the same open `SKILL.md` standard
gald3r ships, so skills are directly portable with no adaptation.

## C.R.A.S.H. capability grid

| | Capability | Native? | What gald3r gets here | The gap |
|---|---|:---:|---|---|
| **C** | Commands | ✅ | 40+ built-in slash commands (`/init` `/review` `/agent` `/skills` `/mcp`); user-defined Custom Prompts (`~/.codex/prompts/`) install as `$`-invoked slash commands | Custom Prompts are deprecated — Codex steers reusable invocable workflows toward skills instead |
| **R** | Rules | ✅ | `AGENTS.md` instruction hierarchy (always-on rules), persistent Memories (`~/.codex/memories/`), and execpolicy files for hard allow/block | None — gald3r rules load as first-class instruction files; instruction convention is `AGENTS.md`, not `CLAUDE.md` |
| **A** | Agents | ✅ | Custom subagents as standalone TOML (`~/.codex/agents/` or `.codex/agents/`) with model / sandbox / mcp / skills config; built-in `default` / `worker` / `explorer`; managed via `/agent` | Subagents are not auto-spawned — Codex only creates them on explicit request (natural language or `/agent`) |
| **S** | Skills | ✅ | Agent Skills — `SKILL.md` directories under `.agents/skills` (repo) and `$HOME/.agents/skills` (personal), invoked explicitly or implicitly by description | None — same open Agent Skills standard as Claude; gald3r `SKILL.md` files are directly portable |
| **H** | Hooks | ✅ | Codex Hooks via `hooks.json` or inline `[hooks]` in `config.toml`, spanning 10 lifecycle events (SessionStart, Pre/PostToolUse, PermissionRequest, Pre/PostCompact, UserPromptSubmit, Subagent lifecycle, Stop) | Non-managed hooks require explicit user trust; only managed (enterprise) hooks run automatically |

_Legend: ✅ native · ⚠️ partial / approximated · ❌ no native mechanism · ❓ unverified_

**Beyond C.R.A.S.H. — MCP: ✅** Native Model Context Protocol via `[mcp_servers.<name>]`
tables in `config.toml` (stdio + HTTP), with `codex mcp add` and per-tool approval modes;
`/mcp` lists active servers. gald3r's MCP backend connects directly.

## Adoptable extras (non-C.R.A.S.H.)

Platform-native strengths gald3r can lean on, and which need wiring:

| Feature | Status | gald3r fit |
|---|:---:|---|
| Codex Plugins (`/plugins`) | ⚙️ needs customization | Packaging surface for bundling gald3r extensions; wiring optional |
| Codex Apps (`/apps`) | ✅ present | Extra installable-app surface alongside plugins/MCP; no gald3r work required |
| `config.toml` (global + project-scoped `.codex/config.toml`) | ✅ present | Central control plane for model, sandbox/approval, MCP, hooks, and agent overrides |
| Subagent workflows + `PLANS.md` exec-plan pattern | ⚙️ needs customization | Could drive gald3r multi-agent and multi-hour structured workflows |

## The ceiling, and what's beyond it

gald3r runs at full strength on this platform — commands, rules, agents, skills, and hooks all map onto native mechanisms, so the framework installs without compromise. As third-party adaptation goes, this is the high end: nothing here has to be approximated.

But adaptation, however clean, is still gald3r living as a guest inside someone else's tool. The native build goes further — **gald3r_agent**, running on the **gald3r throne** over the **gald3r_world_tree** — where these primitives aren't mapped onto a host, they *are* the substrate. Same framework, no host in between.

> ### gald3r_agent — coming soon. 🌳

---

<sub>Capabilities verified against the platform's official documentation on 2026-06-02, and
re-verified each release via the gald3r platform-docs crawl. This report describes gald3r's
third-party adaptation surface; it is not an endorsement or critique of the platform itself.</sub>

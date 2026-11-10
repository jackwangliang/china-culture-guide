# 11 — Agent setup, live search and gate verification

Use this guide when installing the skill on a new agent, when the search gate unexpectedly fails, or when a user asks "why did it refuse to answer?". It is an **operational SOP** — finite, checkable steps — not cultural content. The gate itself is defined in `framework.md` Step 0a and `evidence.md`.

**Note on filenames:** `AGENTS.md`, `TOOLS.md`, `config.toml` and `requirements.toml` mentioned below are files in the **host agent's workspace or home directory**, not files in this repository. They are yours to create or edit; this skill never writes to them.

## What "search available" actually means

The gate does **not** pass merely because a tool named `web_search`, `WebSearch` or `Browser` exists. It passes only when all four hold:

1. A query can be sent.
2. Results come back **from the live web**, not only from a cached or pre-built index with no readable pages.
3. At least one primary or institutional source can be **opened and read**, so a date, quotation or causal claim can be checked.
4. The result set is not entirely C-tier aggregator pages (apply the source-cluster check in `evidence.md`).

If any of these fails, treat it as **gate failed** and use the NO-SEARCH CONTRACT. A tool that exists but yields no readable sources is functionally offline for this skill.

## Per-platform setup

Paths and flags change between releases; verify against the agent's own documentation and its skill list. These notes describe the defaults that most often cause a false "I have search" assumption.

### Codex CLI (OpenAI)

| Item | Note |
|---|---|
| Skill location | `$CODEX_HOME/skills/china-culture-guide/` (default `$CODEX_HOME` is `~/.codex`). Some versions and installers also read `.agents/skills/` (project) or `~/.agents/skills/` (personal). **Check `/skills` inside Codex** — that list is authoritative, and identically named skills are not merged. |
| Install | `git clone <repo> "$CODEX_HOME/skills/china-culture-guide"`, or `$skill-installer <owner>/<repo>/china-culture-guide`. Explicit invocation uses `$china-culture-guide`. |
| Live search | `web_search` in `~/.codex/config.toml` accepts `cached` (**default** — an OpenAI-maintained index, no live fetch), `live`, `indexed` (newer builds) and `disabled`. Set `web_search = "live"` or start a session with `codex --search`. |
| Sandbox | Shell network is off by default in read-only and workspace-write sandboxes. `sandbox_workspace_write.network_access = true` may be needed for fetches outside the built-in search tool. |
| Enterprise override | A `requirements.toml` can restrict allowed web-search modes regardless of user config. If `--search` has no effect, check this. |
| Failure sign | The agent says it "searched" but produces no source names or dates, or every citation is a vague paraphrase. Likely `cached` mode. |

`description` is the only field loaded at startup in every implementation. Codex caps the initial skill list at roughly 2% of the context window (or 8000 characters when unknown) and shortens descriptions first when many skills are installed — which is why the live-search requirement is the **first sentence** of this skill's description.

### OpenClaw

| Item | Note |
|---|---|
| Skill location | `~/.openclaw/skills/china-culture-guide/` or the workspace `./skills/` directory. Workspace skills take precedence. `clawhub install` defaults to `./skills` unless `--workdir` / `CLAWHUB_WORKDIR` says otherwise. |
| Verify | `openclaw skills list`, then start a new session — skills load at session start. |
| Live search | **Not built in by default.** Install a Web Search or Browser skill, or configure an MCP search server. Without one, the cultural gate must fail. |
| Tool rules | Workspace `TOOLS.md` can record when search should be used; `AGENTS.md` holds always-on operating rules. A short line such as "cultural questions in china-culture-guide require live search; never answer them from memory" makes the gate explicit. |
| Publishing | ClawHub is the public OpenClaw skill registry (`clawhub` CLI: search / install / publish). Publishing there is optional and separate from the GitHub release. Review any third-party skill's files before installing. |
| Failure sign | The agent has browser/terminal tools but no search skill, and quietly answers from recall. Add a search skill or accept the NO-SEARCH CONTRACT. |

### Claude Code, WorkBuddy and other SKILL.md agents

| Item | Note |
|---|---|
| Skill location | `~/.claude/skills/china-culture-guide/`, `~/.workbuddy/skills/china-culture-guide/`, or the client's documented skills directory. The repository root is the skill folder. |
| Live search | A `WebSearch` / `WebFetch` tool, a browser tool, or an MCP search server. If the client has no retrieval tool at all, cultural answers must use the NO-SEARCH CONTRACT. |
| Compatibility | Only `name`, `description`, `license`, `compatibility` and `metadata` from the SKILL.md frontmatter are standard. Clients ignore unknown fields. |

### Why there is no `allowed-tools` field

The open Agent Skills specification lists `allowed-tools` as **experimental**, with support that varies by implementation. More importantly, tool names are not portable: Codex uses `web_search`, many clients use `WebSearch` / `WebFetch`, and OpenClaw exposes search as an installable skill or MCP server. Hard-coding one name would lock the skill to one product, and on a client that enforces the field it could even block the tools the gate needs.

The requirement is therefore declared in three platform-neutral layers:

1. **`compatibility`** in the frontmatter — the standard field for environment and network requirements.
2. **The first sentence of `description`** — the only metadata loaded at startup, so the agent sees the requirement before it activates the skill.
3. **The answer-time gate** in `framework.md` / `evidence.md` — a prompt-level convention the agent applies, checking what can actually be retrieved rather than what a config file promises.

Do not add `allowed-tools`, a Codex-only `openai.yaml`, or any other product-specific manifest. Other agents either ignore them or, worse, enforce them inconsistently.

## Four-step verification after installation

Run these once on a new agent before trusting the skill with a real question.

1. **Discovery.** Ask the agent to list its skills. `china-culture-guide` should appear with a description that still begins with the live-search requirement (if the client truncates descriptions, the first sentence should survive).
2. **Positive test.** Ask: *"When did stir-frying start, and what is the earliest written record?"* A passing answer names a source type and a date, separates "first recorded" from "became common", and includes an uncertainty note. If it reads like a confident essay with no sources, search did not actually run — fix the platform's search configuration.
3. **Negative test.** **Actually disable retrieval in the client** (Codex: `web_search = "disabled"`; OpenClaw: remove the search skill; MCP clients: disconnect the search server), then start a fresh session and ask the same question again. A passing answer uses the NO-SEARCH CONTRACT: a short refusal, the term with pinyin, questions to check later, 2–3 Chinese keywords, one next action — **and no dates, quotations or lens sections**. Merely asking for an offline answer while the search tools are still enabled is a **simulation, not a valid negative test**: it checks whether the agent follows instructions, not whether the platform is configured correctly. State which one you ran.
4. **Leak check.** Re-read the negative answer. Any "generally", "traditionally", "because…" or a numbered list of historical stages means the gate leaked. Treat that as a bug in the host configuration, not as an answer.

## Boundaries

- Configuration keys, default paths and registry names change between releases. Confirm in the agent's own docs; do not add unverified flags to this file.
- This guide never lowers the gate. If a platform cannot do live retrieval, the correct outcome is the NO-SEARCH CONTRACT, not a relaxed rule.
- **Known limitation.** The gate is a prompt-level convention with no runtime enforcement. This skill ships no executable code, so a host agent that ignores it can emit an unverified essay with no visible failure. The four-step check above is the only mitigation, and its negative step is meaningful only when retrieval is genuinely disabled. Do not describe the gate as "enforced" in docs or issues.
- Publishing to a registry is optional and is the user's decision. This skill does not require an account, an API key or any paid service.

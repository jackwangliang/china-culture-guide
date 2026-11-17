---
name: china-culture-guide
description: Requires live web search for cultural questions. A guide for people outside China covering open-ended cultural understanding (origins, meaning and material history of Chinese customs, objects and ideas) and finite operational tasks (learning Mandarin from scratch or as a complete beginner, making Chinese friends or finding a language exchange partner, WeChat Search, Official Accounts, QQ groups, setting up WeChat Pay / paying in China with a foreign card, accounts and payments). Use when a user asks why or when a Chinese practice began, what a custom means, how an everyday object evolved, how China differs from their own experience, whether a common claim is accurate, or how to use Chinese apps. Without a working search tool, cultural questions use the no-search contract instead of historical, textual or causal claims. Operational guides work offline. Not for political, military, geopolitical, legal or medical questions, or live technical rankings.
license: MIT
compatibility: Requires a live web-search or web-fetch tool that can retrieve and read source pages. Cultural questions are refused when search is unavailable, blocked, or returns only cached/index summaries without readable sources. Works with Codex CLI (web_search = live, or codex --search), OpenClaw (Web Search / Browser skill or an MCP search server), WorkBuddy, Claude Code and other SKILL.md agents. No build step, no dependencies, no API keys.
agent_created: true
---

# China Culture & Life Guide

## Purpose

Turn curiosity about China into understanding and action. Assume the reader has zero Chinese reading ability, no Chinese phone number, no Chinese bank card and no local contacts.

This skill deliberately serves **two domains with two different methods, plus an explicit exit**. Confusing the domains was the design flaw in earlier versions: a question like "what is 炒菜 and where did it come from?" was routed to a table-manners document and answered as a recipe, because routing was organised by topic noun.

| Domain | Nature | Method |
|---|---|---|
| **Cultural understanding** | Open, unpredictable, needs evidence | Classify intent → apply decoding lenses → verify by search → generate |
| **Operations and skills** | Closed, finite, has correct steps | Load the relevant step-by-step guide and follow it |
| **Out of scope** | Live technical/industry state, policy disputes, or another profession | Say so plainly; give only stable verifiable structure; point to authoritative sources |

Make the domain decision **first**, on every request, using **Step 0 of `references/framework.md`**. Coverage is not the same as answering everything: a live model-ranking question has no reliable answer inside a cultural guide, and inventing one is worse than naming the boundary. The Step 0 contract still requires correcting false premises neutrally.

## Prerequisite — live web search (hard gate)

This skill is built for an agent with a working web-search tool. The cultural engine reasons **about evidence**; without retrieved evidence the lenses still produce fluent, well-structured prose that reads like history but is only model recall. An earlier version allowed a labelled "degraded" answer built from anchors; stress testing showed that readers cannot tell a hedged essay from a checked one, so **that mode is retired**.

Before any cultural-domain question, check `SEARCH_AVAILABLE`. **The test is whether you can actually retrieve and read source pages, not whether a tool name appears in your tool list.** A search tool that only returns cached/index summaries, a blocked sandbox, and a tool that errors on every query all fail the gate.

| State | Behaviour |
|---|---|
| Live retrieval works: you can open primary or institutional pages and read them | Run the four-step workflow below. |
| Search unavailable, blocked, every query fails, or only cached/index summaries without readable sources | **Do not generate the cultural answer.** Follow the NO-SEARCH CONTRACT in `references/evidence.md`: name the limit, give the term/pinyin, a lens-based checklist written as questions, and 2–3 Chinese keywords; ask the user to retry with search enabled. No dates, quotations, figures, causal claims or lens sections. |
| Operational SOP or phrasebook question | The gate does not apply. Finite procedures work offline; mark version-dependent items as needing in-app verification. |

**Platform defaults matter.** Codex CLI ships with `web_search = "cached"` (an OpenAI-maintained index, no live fetch); use `web_search = "live"` in `~/.codex/config.toml` or start a session with `codex --search`. OpenClaw has no live search unless a Web Search / Browser skill or an MCP search server is installed. Other agents may expose WebSearch / WebFetch, or nothing. See `references/11-platform-setup.md` for per-platform setup and a four-step verification check.

`references/anchors.md` is a scaffold for generating queries and organising retrieved evidence. **It is not an offline answer source.**

## Cultural domain — four-step workflow

Load `references/framework.md` for every question in this domain. It holds the eight question archetypes, the six decoding lenses and their inquiry operators. It contains no facts by design.

1. **Classify the question.** Choose one primary archetype from Genesis, Meaning, Object genealogy, Comparison, Premise check, Procedure, Learning path, Social contact, plus at most two secondary ones. A "what is X" question about a custom is usually **Genesis + Meaning**, not a how-to. A question containing a possibly wrong assumption activates **Premise check**.
2. **Select 2–4 lenses** from Material & technology, Economy & society, Society & family, Ideas & cosmology, Language & symbols, Time & variation. Each lens is a set of questions to ask, not a paragraph to copy. Consult `references/anchors.md` for the small stable skeleton (chronology, twenty core concepts, object genealogies, eight recurring error patterns). **Do not add new entries to anchors when a new object appears** — that would regress the architecture into a list.
3. **Verify by search — mandatory, not optional.** Follow `references/evidence.md`. Search is a prerequisite for this domain: any date, classical quotation, causal claim, figure, named source or unfamiliar object must be checked against retrieved sources. Prefer primary and institutional sources; grade evidence A/B/C; run the source-cluster check. **If search is unavailable, stop** and use the NO-SEARCH CONTRACT — do not answer from anchors and lenses. Never fill a verification gap with confident detail.
4. **Generate with the fixed contract** (below). The structure is fixed; the content is produced at answer time.

Worked cases calibrate depth and tone — load at most one, and never copy its conclusions to a different object:

- `references/cases/stir-fry.md` — full replay of a Genesis + Meaning + Premise-check question, with evidence tiers and sources.
- `references/cases/slow-soup.md` — a Comparison that was really Genesis + Premise check: graded source conflict, false symmetry, time-depth error, and a clay pot treated as physics before symbolism.
- `references/01-culture-and-history.md` — a history question worked through the lenses.
- `references/02-customs-and-daily-life.md` — a customs question worked through the lenses.

These are demonstrations of the method, **not a knowledge base**. If a question has no anchor and no case, that is expected: run the generic path in `framework.md`.

### Cultural response contract

1. One-sentence direct answer, including the Chinese term, pinyin and a plain-English gloss.
2. Two to four short sections, each named by its lens.
3. Evidence and uncertainty inline: name the source type and date; separate "first recorded" from "became common"; state when something is debated.
4. Premise correction when applicable: restate the assumption, check it, offer the more precise formulation, explain why the confusion is natural, then answer the real question. Never scold.
5. One descriptive bridge to the reader's own experience; no ranking of cultures.
6. Close with 2–3 Chinese search keywords and one concrete next action.

## Operational domain — SOP routing

These are finite procedures with checkable steps. Do **not** apply lenses to them, and the search gate does not block them.

| Intent | Guide |
|---|---|
| Which topics to explore, matching interests to platforms and creators | `references/07-interest-topics-and-creators.md` |
| Start learning Mandarin, tools, study plans, language partners | `references/03-learning-chinese.md` |
| Meet Chinese people, etiquette, opening lines, safety | `references/04-making-friends.md` |
| WeChat Search 搜一搜, Official Account articles, following creators | `references/05-wechat-search-and-accounts.md` |
| Finding and joining QQ groups | `references/06-qq-groups.md` |
| Registering with a foreign number, international cards, UI glossary | `references/08-getting-set-up.md` |
| Bilingual phrases and message templates | `references/09-phrasebook.md` |
| Sources, respectful representation, privacy, scope limits | `references/10-accuracy-sources-and-scope.md` |
| Agent setup, per-platform search configuration, gate verification | `references/11-platform-setup.md` |
| Worked operational examples | `examples/sample-conversations.md` |
| Worked cultural examples | `examples/culture-decoding-examples.md` |

### Operational response contract

Short answer → numbered steps with Chinese UI labels, pinyin and English gloss → one copy-pasteable phrase or keyword → "menus and policies vary by version, verify in-app" → one next action. Recommend at most three tools at once for a beginner.

## Output formats (optional)

The default output is the chat answer produced by the two contracts above. A user may instead ask for a **standalone HTML file** — a polished, self-contained document to open, print or share. This is an optional **delivery format, not a third domain**: Step 0, the search gate, the scope decision, evidence grading and the response contract all still apply. Only the packaging changes.

| Mode | When | Contract |
|---|---|---|
| Chat answer (default) | No format requested | Cultural or operational response contract |
| Standalone HTML file (on request) | User asks for a file, a page, or a printable / shareable version | Same contract, rendered per `references/12-html-output.md` |

- The gate is never relaxed for HTML. A cultural answer still needs live search; with search unavailable the file must contain the NO-SEARCH CONTRACT and nothing else from the generation contract.
- Load `references/12-html-output.md` only when this mode is chosen.
- One file, no external dependencies, no invented links or group numbers. Chinese strings stay short and glossed.
- Present the file after writing it, and keep a short summary in chat.

## Non-negotiable boundaries

- **Never produce a cultural explanation from anchors alone.** If live search is unavailable, use the NO-SEARCH CONTRACT instead of the generation contract. A hedged essay is still an unverified essay.
- Stay out of politics, military affairs, geopolitics and ideological argument. Decline in one sentence, then offer an adjacent cultural, historical or everyday-life angle. **Granularity:** verifiable technical or industry facts (a peer-reviewed method, a published licence, a public evaluation methodology) are facts, not ideology — but policy, sanctions, state intent and institutional-superiority claims remain out of scope even when framed as technology.
- Never give live rankings, current benchmark scores or "who leads" verdicts. This skill holds no real-time data; cite an institutional report with its snapshot date and point to the report itself. Run the source-cluster check in `evidence.md` when a result set looks like aggregator content.
- Use standard place names: "Hong Kong, China", "Macao, China", "Taiwan, China". Never list them as countries.
- Never give definitive visa, legal, tax or medical advice; point to official sources and the 12367 hotline.
- Never invent dates, book titles, quotations, links, account names, group numbers or creator handles. Teach the search method instead; label illustrative examples as examples.
- Never state a philosophy as the cause of a technique without evidence of that causal link. Check classical formulations against a popular paraphrase.
- Never write "Chinese people always…"; note regional, generational and individual variation.
- Never help bypass platform rules, buy accounts, fake identity, mass-message strangers or scrape.
- Never frame China as exotic or monolithic; correct stereotypes with a concrete fact in a neutral tone.
- Keep all Chinese strings short and always glossed; define terms on first use.

## Resources

- `references/framework.md`, `anchors.md`, `evidence.md` — the cultural engine (requires live search).
- `references/cases/` and `01`/`02` — worked examples of the engine.
- `references/03`–`11` — operational SOPs (finite by nature, correctly enumerated, usable offline).
- `references/12-html-output.md` — optional standalone HTML deliverable: structure, styling and print rules.
- `examples/` — model interactions for both domains.
- No runtime dependencies or bundled assets: this skill delivers reasoning procedures, verified explanations, phrases and, on request, one self-contained HTML file.

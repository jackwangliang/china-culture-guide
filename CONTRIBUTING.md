# Contributing

Thanks for helping make China easier to understand for people outside it. Please read the **architecture rules** first — most useful contributions here are improvements to the reasoning method, not new facts.

## The architecture in one paragraph

This skill makes three decisions. **Step 0** is a **hard search gate** first, then a scope check: live technical/industry state, policy disputes and other professions are out of scope, and cultural questions **cannot be answered without live web search**. **Cultural understanding** is open-ended: handled by `references/framework.md` (eight question types × six decoding lenses), `anchors.md` (a small, stable skeleton used to generate queries and organise evidence) and `evidence.md` (search, the NO-SEARCH CONTRACT, evidence tiers, source-cluster checks, uncertainty). **Operations** are finite: WeChat Search, QQ groups, registration, learning plans, phrases and agent setup are step-by-step SOPs in `03`–`11`, and they work offline. `12-html-output.md` is an optional **delivery-format spec**, not an SOP and not a third domain — the same gate and contracts apply to an HTML file. Coverage comes from **types × lenses × live evidence**, not from the number of entries written down — and knowing when to decline is part of coverage. The live-search requirement is declared in the standard `compatibility` frontmatter field and the first sentence of `description`; there is deliberately no `allowed-tools` field.

## What belongs here

- New **inquiry operators** for a lens, or a better question type, in `framework.md`.
- A sharper **Step 0 scope test**, a new premise subtype, or a better out-of-scope response pattern.
- Worked cases that demonstrate the method on a new kind of question (`references/cases/`).
- A better **no-search checklist**: clearer verification questions, better Chinese keywords, more useful institutional sources to point at.
- **Verified updates to `11-platform-setup.md`** when an agent changes its skill path, search defaults or config keys. Include the source and the version you checked.
- Corrections to outdated UI labels, fees, limits or policy facts, with a source.
- Verified sources added to `10-accuracy-sources-and-scope.md`.
- Better uncertainty wording, better premise-check examples, better search-query recipes.
- Better **source-cluster heuristics** for topics where aggregator pages dominate search results.
- Clearer rules for **undated sources** and for **a single source that contradicts itself**, in `evidence.md`.
- Improvements to the optional **HTML output spec** in `references/12-html-output.md` — keep it self-contained, dependency-free and gate-preserving.
- Bilingual phrases with pinyin and a plain-English gloss, in `09-phrasebook.md`.
- Translations of README and guides into other languages.

## What does not belong here

- **Long lists of cultural facts, objects, festivals or "10 things about X".** That is the old design and it does not scale. A new user question about a new object does not earn a new entry.
- Additions to `anchors.md` in response to a single question. That file must stay a small skeleton; if it starts becoming an encyclopaedia, the architecture has regressed.
- **Offline cultural answers, "degraded essays", or any proposal to restore a fallback mode.** An answer built from anchors and model recall with a disclaimer is still an unverified answer. The NO-SEARCH CONTRACT is the only permitted behaviour when search is unavailable.
- **Wording that implies the search gate is technically enforced** ("runtime enforcement", "guaranteed", "blocked by the system"). It is a prompt-level convention the host agent must honour; describe it accurately, including in README and issue text.
- **External dependencies in the HTML output**: CDN stylesheets, web fonts, JavaScript libraries, trackers, iframes or remote images. The file must open offline from `file://`.
- **Product-specific manifests**: `allowed-tools`, a Codex-only `openai.yaml`, hard-coded tool names (`web_search`, `WebSearch`, a specific MCP server) or a per-client fork. The specification marks `allowed-tools` experimental, and tool names are not portable. Use `compatibility` plus the answer-time gate instead.
- **Live rankings, current benchmark scores, product specs or "who leads" verdicts**, especially when the only sources are aggregators. Point to an institutional report with its date instead.
- **Stretching the cultural lenses to answer an out-of-scope question.** A confident-sounding essay about current AI capability is not cultural understanding.
- Politics, military topics, geopolitics, sanctions, state intent or ideological argument. Deliberate scope limit, not an oversight. Verifiable technical facts themselves are fine.
- Stereotypes ("Chinese people always..."), exoticising language, or claims about a single "Chinese mindset".
- Definitive visa, legal, tax or medical advice. Link to an official source instead.
- Invented account names, group numbers, article titles, creator handles, dates, book titles, quotations or URLs. Illustrative examples must be labelled as examples.
- Instructions for buying accounts, borrowing IDs, bypassing verification, mass-messaging, scraping, or any other platform-rule violation.
- Personal data, screenshots containing private chats, or private group invite links.

## Content rules

1. **Simple international English.** Short sentences, no idioms that need a dictionary. Define every Chinese term on first use.
2. **Always gloss Chinese strings.** Format: `搜一搜 / sōu yī sōu / "Search"`. Pinyin with tone marks.
3. **Check the search gate, then Step 0, then the domain.** Cultural questions require live search; if it is unavailable, use the NO-SEARCH CONTRACT and stop. Out of scope gets the out-of-scope contract; a cultural question gets lenses and evidence; an operational question gets numbered steps. Never answer "why does this custom exist" with a how-to list, and never turn a button-location question into an essay.
4. **Mark time-sensitive facts.** App menus, fees, limits and entry policies change. Add "verify in-app / on the official site" and a source link. A ranking is a dated snapshot, never a verdict.
5. **Grade your evidence — and inspect the whole result set.** Follow the A/B/C tiers and the source-cluster check in `evidence.md`; never cite an encyclopaedia or blog as authority for a date or quotation, and never treat a crowd of agreeing aggregators as corroboration. Separate "first recorded" from "became common".
6. **Check the premise.** If a question assumes something unverified, correct it gently and still answer the underlying question. Watch for false symmetry, time-depth errors and single-scalar "who is ahead" framing. Without sources, do not attempt correction — put it on the verification checklist.
7. **Use correct place names.** "Hong Kong, China", "Macao, China", "Taiwan, China". Never list them as countries.
8. **Keep SKILL.md lean.** It holds the search gate, scope check, domain decisions, the four-step workflow and the SOP routing table only.
9. **Give one next action.** Every guide and example should end with something a reader can do in 15 minutes.
10. **Treat `anchors.md` as a query generator.** Never cite it as the source of an answer, and never use it to reconstruct an explanation when search fails.
11. **Keep the frontmatter portable.** `name` and `description` are required; `license`, `compatibility` and `metadata` are optional standard fields. Unknown fields are ignored by other clients. Keep the live-search requirement first in `description`, because that is the only metadata loaded at startup and some clients truncate long descriptions.
12. **Handle undated sources explicitly.** Write `undated` in the answer; never let an undated page support a date, a chronology, a "first recorded" claim or a popularisation date. See `evidence.md`.
13. **Never silently reconcile a source that contradicts itself.** Present both statements with the source name and date and name the inconsistency, even when the source is A/B tier. See `evidence.md`.
14. **An HTML file is a format, not a domain.** Never relax the search gate, the scope decision or the response contract to fill a page. Follow `references/12-html-output.md`.

## Suggested PR process

1. Open an issue describing the gap, the outdated fact or the weak lens — and include a source where relevant.
2. For a new worked case, add one file under `references/cases/` and link it from SKILL.md. Do not expand `anchors.md` or the discovery menu to accommodate it.
3. For translations, add a language-suffixed file (e.g. `README.es.md`) and link it from the English README.
4. Check that no fabricated names, dates or links were introduced, that no out-of-scope content slipped in, and that no example quietly answers a cultural question without evidence.
5. If you changed the frontmatter, run the reference validator and verify that the skill still loads on at least two different agents.
6. Describe the change in one or two sentences.

## Style check before submitting

- Did the answer stay inside scope, or did it quietly answer a question this guide cannot verify?
- **Did the answer come from retrieved sources — or from anchors / memory because search was unavailable?** In the second case, it should not be an answer at all.
- Would a person who has never used WeChat understand every operational step?
- Is there at least one copy-pasteable phrase or keyword?
- Is anything stated as permanent that actually changes?
- Did the answer verify its facts, or quietly rely on memory — or on a cluster of similar-looking sites?
- Does the change still work on Codex CLI, OpenClaw and a plain `SKILL.md` client, or did it quietly assume one product's tool names or paths?
- Is the tone neutral, warm and free of clichés?

By contributing, you agree that your contribution is licensed under the MIT License in this repository.

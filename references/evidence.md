# Evidence, Search and Premise Checking

This file makes **live verification a hard prerequisite** of the skill. Load it for every cultural question classified as Genesis, Meaning, Object genealogy, Comparison or Premise check in `framework.md`.

## Prerequisite: live search (hard gate)

This skill has **no offline answer mode**. Earlier versions allowed a labelled "degraded" answer built from `anchors.md` plus lenses, with no dates or quotations. Stress testing exposed the flaw: such an answer is structurally perfect — definition, lens sections, a bridge, a next action — while every historically meaningful sentence is unverified model recall. A reader cannot tell a hedged essay from a checked one. **A confident essay about history without sources is worse than a short refusal.**

| Situation | Behaviour |
|---|---|
| **Live retrieval available** — queries run and primary / institutional pages can be opened and read | Verify each claim. Primary or institutional sources first. Then run Steps 1–4 in `framework.md`. |
| Search unavailable, blocked, every query fails, **or results are only cached / index summaries with no readable source pages** | **NO-SEARCH CONTRACT** (below). Do not produce the cultural answer. A search tool that exists but yields no verifiable sources is functionally offline; see `11-platform-setup.md`. |
| Operational SOP or phrasebook question | The gate does not apply. Follow the SOP; time-sensitive items must be marked "verify in-app" rather than asserted. |
| Out-of-scope / live-state question | Out-of-scope contract in `framework.md` Step 0; never quote a current number from memory or from aggregators. |

### NO-SEARCH CONTRACT

When the gate fails, deliver **only** the following, in this order:

1. **One plain sentence:** say this question needs historical or textual evidence and that sources cannot be checked right now, so you will not guess. No apology loop, no lecture about accuracy.
2. **Safe language layer:** the Chinese term, pinyin and a literal gloss only — no claim about origin, age, meaning-in-context or symbolism.
3. **A verification checklist written as questions**, derived from the relevant lenses: "Which material prerequisites had to exist first?", "Is there a contemporary written record, or only a later one?", "Did this begin as an elite, ritual or household practice?", "Is the modern form the same as the old one?". These are what the user — or the agent after reconnecting — should check. **Never phrase them as findings.**
4. **2–3 Chinese search keywords** the user can paste into 搜一搜 or a search engine.
5. **One next action:** retry in a search-enabled session, or open an institutional source (museum, university, official help centre) directly.

**Forbidden in no-search mode:** dates, dynasties, reigns, "first recorded in…", classical quotations, book titles, percentages, prices, named studies, causal claims ("because…"), "scholars generally agree", lens-named explanatory sections, bridges that assert a cultural contrast, and any part of the generation contract that presents an interpretation as an answer. Do not paraphrase the refusal into an essay. Do not "answer from general knowledge" after the disclaimer.

Anchors and lenses remain useful **as a query generator and a checklist**. They are not a substitute for evidence.

## Which claims must be verified individually

Once the gate passes, check each of these against retrieved sources:

- Any date, dynasty, reign, century or "first recorded in…" claim.
- Any quotation from a classic, or a claim that a text says something.
- Any causal claim of the form "X appeared because of Y".
- Any figure (percentages, prices, limits, counts, country lists).
- Any question whose premise might be wrong.
- Any question about a named object, site, person or work not in `anchors.md`.
- Any concept with a well-known popular misreading (五行, 面子, 火候, "5,000 years").

If a mandatory claim cannot be verified even with search, say so inline and leave it out of the answer rather than approximating it.

## Constructing queries

Chinese queries outperform direct English translations for historical and textual questions. Build four kinds and compare them.

| Kind | Pattern | Worked example (the 炒菜 question) |
|---|---|---|
| Academic Chinese | `object + 起源/演变/考/普及` | `炒菜 起源 铁锅 植物油` |
| Primary text | `书名 + 篇名 + 关键词` | `齐民要术 炒鸡子法 麻油` |
| Institutional / archaeological | `机构 + 主题` | `考古 分餐制 合食制 桌椅 唐代` |
| Conceptual | `概念 + 经典 + 原文` | `易经 既济 水在火上 吕氏春秋 本味 火之为纪` |
| English supplement | `topic + history / archaeology / scholarship` | `Chinese stir-fry origin iron wok Song dynasty` |

Practical rules:

- Use **short noun phrases**, not translated full sentences.
- Add a dynasty or book name to separate early evidence from later commentary.
- Search the classical formulation *and* the popular claim separately — they often disagree, and the gap is the interesting part.
- Avoid relying on a single aggregator page; find the institution, the excavation report or the text behind it.
- Record which query produced which claim, so the answer can be audited.
- If every query fails or returns nothing usable, treat it as **search unavailable** and fall back to the NO-SEARCH CONTRACT. Retrieving nothing is not permission to use recall.

## Evidence tiers

| Tier | What it is | How to use it |
|---|---|---|
| **A** | Excavated objects and excavation reports; original classical texts; official sources (government, app help centres, testing bodies); academic institutional publications | May be stated directly, with date and name |
| **B** | Scholarly research summarised by established media; museum or university public scholarship; authoritative surveys | Attribute explicitly ("according to…", "a 2025 survey reported…"), state the population and date |
| **C** | Encyclopaedia entries, blogs, self-media, forum answers, marketing pages | **Leads only.** Use to discover keywords, then verify upward. Never cite as the basis for a date, quotation or figure. |

When tiers disagree, prefer A, then show the disagreement: "The text records X in the 6th century, but when it became common is still debated." Never average conflicting claims into a confident middle date.

## Source-cluster check (before trusting a result set)

A/B/C grades rate **one source at a time**. On live technical and industry topics the entire result set can be C-tier — SEO pages, aggregators, self-media, AI-generated listicles — and these pages quote one another. Ten bad sources agreeing is not corroboration; it is **false consensus**.

Run this check before writing any number into an answer:

1. **Cluster the hits.** Are they mostly the same kind of site? If no institutional, primary or peer-reviewed source appears at all, treat the whole set as unverified.
2. **Test for contradiction.** If the same quantity appears as 1%, 2.7%, 8.5 points and 21 Elo points across sources claiming the same date, the number is not a fact with error bars — it signals unstated definitions or fabricated content. Do not average them, do not pick a plausible middle, and do not quote any of them.
3. **Test entity plausibility.** Product names, version numbers and organisation names that do not appear in the primary source should be dropped, not repeated.
4. **Escalate to a named primary source.** Prefer the institution's own report, the journal article, the official documentation; restrict the search to that domain if needed.
5. **If no primary source can be found**, say the current state could not be verified and answer only the stable structural part, following the out-of-scope contract in `framework.md` Step 0.

## Live-state claims

Any claim about *right now* — rankings, prices, model versions, policies, limits — is a **snapshot**, never a verdict.

- Always attach the observation date and the measurement definition ("as of March 2026, on the Arena Elo leaderboard").
- State when the source itself warns that the measure is unreliable (benchmark saturation, invalid question rates, platform-adaptation effects).
- Describe capability as **multi-dimensional**; refuse frames that compress it into a single "who is ahead / who surpassed whom" axis.
- Never turn a trend into a permanent property ("always behind", "can never surpass"). Those are unfalsifiable and age badly.
- When the observation is months old, say so instead of presenting it as current.

## Handling conflict and uncertainty

- Separate **first attestation** from **widespread adoption**. Say so explicitly.
- Where scholarship has no consensus, say so in one plain sentence and give the range of views.
- Where a source is describing elite or ritual practice, do not extrapolate to ordinary households.
- Where a modern revival is presented as ancient, name it as a revival.
- Mark anything that changes (fees, UI, policy, opening hours) as version-dependent.
- **One source contradicting itself.** If the same institutional or primary page makes two incompatible statements — for example "the technique appeared in the Tang" alongside "the earliest record is in the 6th century" — do **not** silently reconcile them into one timeline. Present both statements, name the source and its date, and say plainly that the source is internally inconsistent. Never average, never pick whichever fits the argument, and never hide the conflict because the source is A/B tier. A high-grade source is still capable of an editorial inconsistency.
- **Undated sources.** If a source carries no publication date, write `undated` explicitly in the answer. An undated page may support a definition or a structural claim, but **must not be used as the basis for a date, a chronological sequence, a "first recorded" claim or a popularisation date**. Grade it one tier lower for any time-sensitive claim. If the date matters, find a dated source or say it could not be verified.

### Uncertainty wording library

| Chinese | English |
|---|---|
| 学界至今没有定论 | "There is still no scholarly consensus on this." |
| 目前普遍认为… | "The common view is…, though it is not settled." |
| 最早的文字记载见于… | "The earliest clear written record is in…" |
| 这不等于当时已经普及 | "That does not mean it was common at the time." |
| 传统上归于…，但缺乏同时代证据 | "Traditionally attributed to…, but without contemporary evidence." |
| 我无法核实这一点 | "I could not verify this; please check [source]." |
| 没联网，这一点我无法核实 | "I can't check sources without a connection, so I won't guess at this." |
| 这个说法来自后来的附会 | "This reading appears to be a later elaboration." |
| 各地、各代差异很大 | "Practice varied greatly by region and period." |

## Premise-check protocol

Users often ask a good question with a slightly wrong frame (e.g. "is 炒菜 derived from 五行相生?"). Handle it without making the user feel corrected.

Check all five premise subtypes listed in `framework.md` Step 1 before searching: a **wrong cause**, a **false symmetry** (both sides of a comparison stereotyped), a **time-depth error** (a recent practice presented as ancient), a **misplaced place or class** (elite, ritual, restaurant or other-region practice treated as everyday life everywhere), and a **single-scalar ranking** (multi-dimensional capability compressed into one unfalsifiable "who is ahead" axis). A single question can fail on several at once.

1. **Restate** the assumption neutrally in one clause.
2. **Check** it against the sources via the mandatory search.
3. **If wrong**, give the more accurate formulation first, then explain briefly why the confusion is natural (a real overlap in vocabulary, a popular simplification).
4. **Answer the underlying question anyway** — the user is after the origin and meaning, not a vocabulary quiz.
5. Never say "that's a misconception" as a full sentence; never lecture.

If the gate has failed, do **not** attempt premise correction: you cannot check a premise without sources. Point the user to the verification checklist instead.

This archetype is what stops the skill from confidently amplifying a plausible-sounding but unsupported claim.

## Citation and fabrication rules

- In conversation: name the source and its date in text; add a link only when it was actually retrieved and is known to resolve. If the source has no date, write `undated` rather than omitting the date or guessing one — see the undated-source rule in "Handling conflict and uncertainty" above.
- Never invent a book title, chapter, quotation, URL, hotline, group number, account name or creator handle. If a source cannot be recalled exactly, describe the source type instead ("a 6th-century agricultural manual") and search for it.
- Never present an illustrative example as a real citation. Label examples as examples.
- Keep the canonical source list in `10-accuracy-sources-and-scope.md`, and add new verified sources there rather than scattering links through answers.

## After searching

Return to `framework.md` Step 4. Organise what was found by lens, add the uncertainty notes, correct any premise, and close with two Chinese keywords plus one next action. Raw search output is never the final answer. If the gate failed, there is no "after searching": end at the NO-SEARCH CONTRACT.

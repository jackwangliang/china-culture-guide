# Decoding Framework — the core of this skill

This file does **not** contain facts about China. It contains the reasoning machinery that turns an unpredictable cultural question into a well-evidenced answer. Load it for every question in the **open cultural domain**.

The old design routed by topic noun ("food" → food document). That fails because questions are infinite and documents are finite, and because "what is 炒菜?" is a question about *origins and meaning*, not a request for a recipe. This design routes by **question type**, then applies reusable **decoding lenses**, then **verifies by search**, then generates content on the spot.

## Step 0 — Gate first, then scope

Two checks, in this order, before classifying intent.

### 0a. The search gate (hard prerequisite)

This framework reasons **about evidence**. Without retrieved evidence, lenses still produce fluent, well-structured prose that reads like history but is only model recall. An earlier version permitted a labelled "degraded" answer built from `anchors.md`; a fourth stress test showed that a hedged essay is indistinguishable from a checked one to the reader, while every historically meaningful sentence in it is unverifiable. **Live search is therefore a prerequisite, not a default.**

| Environment | Cultural domain | Operational domain | Out of scope |
|---|---|---|---|
| **Live retrieval works** — queries run and primary / institutional pages can be opened and read | Proceed to Steps 1–4 | Load the SOP | Out-of-scope contract |
| Search unavailable, blocked, every query fails, **or only cached / index summaries come back with no readable source pages** | **Stop.** Use the NO-SEARCH CONTRACT in `evidence.md`. Do not run Steps 1–4 to produce an answer. | Proceed: SOPs are finite. Mark version-dependent items as unverified. | Out-of-scope contract; never quote a live number from memory |

**A tool that exists is not a gate that passes.** The test is what can actually be retrieved and read. Codex CLI defaults to `web_search = "cached"` (an OpenAI-maintained index with no live fetch); OpenClaw has no built-in search unless a Web Search / Browser skill or an MCP search server is installed. Platform-specific setup and a verification check are in `11-platform-setup.md`.

**The gate is a convention, not a runtime control.** `SKILL.md` and these references are instructions the host agent reads; there is no code that blocks an answer when retrieval is off. A client that ignores the gate can still produce a fluent, unverified essay. Treat "search is unavailable" as an environment fact to be detected, not a role the user is asked to play: a valid negative test disables retrieval in the client configuration and starts a fresh session (see `11-platform-setup.md`). Asking "pretend you are offline" while the tools remain enabled tests the agent's compliance, not the platform's configuration — record which one you ran.

The gate covers the **whole cultural domain**, including questions that look like pure concept explanation. 五行, 面子 and 火候 all have widespread misreadings that only a source check catches. `anchors.md` is a scaffold for generating queries and organising retrieved evidence — **not an offline answer source**. There is no degraded-essay mode.

Lenses may still be used in no-search mode **as a question checklist** (see the NO-SEARCH CONTRACT), never as explanatory sections.

### 0b. Decide whether this skill should answer at all

Three decisions, deliberately separated:

| Decision | Nature | Method | Files |
|---|---|---|---|
| **Cultural understanding** | Open, infinite, needs evidence | Framework + search + generation | `framework.md`, `anchors.md`, `evidence.md`, `cases/` |
| **Operations and skills** | Closed, finite, step-by-step | Standard operating procedures (SOP) | `03`, `04`, `05`, `06`, `08`, `09`, `10` |
| **Out of scope** | Needs live professional data, or belongs to another domain | Say so plainly; give only the stable, verifiable part; point to authoritative sources | none |

Make this decision **first**, before classifying intent. Coverage is not the same as answering everything: recognising a boundary accurately is itself part of coverage. A skill that answers a live benchmarking question with confident cultural prose is worse than one that declines the number.

Route a question **out of scope** when it is primarily about:

- **Live technical or industry state** — current model rankings, benchmark scores, product specs, prices, "who is ahead". These change monthly and this skill holds no real-time data.
- **Politics, military affairs, geopolitics, sanctions, national-security accusations, legal adjudication or medical advice.**
- **A specialised professional domain** (investment, law, engineering, medicine) where a confident general answer is worse than a pointer.

### Out-of-scope response contract

1. One sentence naming the boundary, without apology or lecture.
2. Correct any false premise neutrally — a boundary is not an excuse to leave a wrong assumption standing.
3. Answer only the **stable, verifiable structural part**: concepts, published methods, documented history, with source type and date. Give **no current rankings, scores or "who leads" verdicts**.
4. Name the authoritative sources the reader can check (institutional reports, peer-reviewed papers, official documentation) instead of summarising low-quality aggregators.
5. Close with one concrete next action.
6. Never let the answer drift into policy argument or institutional ranking.

**Granularity rule:** a question mentioning two countries is not automatically geopolitical. Verifiable technical and industry facts — a peer-reviewed method, a published licence, a public evaluation methodology — are facts, not ideology. But the moment the question turns to policy, sanctions, state intent or institutional superiority, stop and redirect in one sentence.

Never treat a cultural question as a lookup. Never treat an operational question as an essay. Never treat an out-of-scope question as a cultural one just because it mentions China.

---

## Step 1 — Classify the question type

Pick **one primary** and at most two secondary archetypes. The type determines which lenses are productive; it does **not** by itself determine whether search is needed (see Step 3).

| # | Archetype | Typical phrasing | What the answer must deliver | Default lenses | Search |
|---|---|---|---|---|---|
| 1 | **Genesis / 起源** | "When did X begin? Why did this habit appear?" | Prerequisites, earliest evidence, diffusion, competing explanations, what is still debated | Material, Time, Economy | Mandatory |
| 2 | **Meaning / 意义** | "What does X mean? Why this way? What does it symbolise?" | The logic, the vocabulary, the world-view behind it | Cosmology, Language, Society | Mandatory |
| 3 | **Object genealogy / 器物** | "How did X evolve? How are X and Y connected?" | Material → form → energy → bodily/social consequences | Material, Time, Society | Mandatory |
| 4 | **Comparison / 比较** | "How is this different from back home / the north / the past?" | A dimension table, not a ranking — unless the question asks *why*, see promotion rules | Any two, chosen to fit | **Claim-driven** |
| 5 | **Premise check / 辨误** | Any question carrying a possibly wrong assumption — a wrong cause, a wrong baseline, a wrong time-depth, a misplaced place or class | Check the premise first, then answer, then explain why the mix-up is natural | Language, Cosmology, Time | Mandatory |
| 6 | **Procedure / 操作** | "How do I search / join / register / pay?" | Numbered steps with Chinese UI labels | none — load the SOP | Gate does not apply |
| 7 | **Learning path / 学习** | "How do I learn Chinese?" | A minimal stack and a routine | none — load `03` | Gate does not apply |
| 8 | **Social contact / 连接** | "How do I make Chinese friends?" | Platform, script, etiquette, safety | none — load `04` | Gate does not apply |

A real question is often a blend. "What is 炒菜, and where did it come from?" = **Genesis + Meaning + Object genealogy**. "Is Chinese food all stir-fried because of 五行相生?" = **Premise check + Comparison + Genesis**.

### Promotion rules

- **A comparison that asks *why* is not a comparison task.** "Why do we make soup in minutes while Chinese people take hours?" is a **Genesis + Premise check** question wearing comparison clothing. Promote it, and use the dimension table only as a way of presenting the result. Answering with a two-column table here would describe the difference without explaining it.
- **Any question naming a concrete object, text, place or date is also an evidence task**, regardless of its primary archetype.
- A "what is X" question about a custom is usually **Genesis + Meaning**, not a how-to.

### Premise subtypes — check all five

The obvious case is a wrong cause (e.g. 五行相生). Four others are easier to miss and more damaging:

1. **Wrong cause** — a philosophy, climate or single invention credited with producing a technique. Check the causal direction.
2. **False symmetry** — both sides of a comparison are stereotyped ("we are fast / they are slow"). Check each side separately; often the real variable is cost, technology or era, not culture.
3. **Time-depth error** — a recent practice presented as an ancient tradition, or an old word used as proof that today's practice is old. Apply the five-stage distinction in L6.
4. **Misplaced place or class** — an elite, ritual, restaurant or other-region practice treated as everyday life everywhere.
5. **Single-scalar ranking / unfalsifiable asymptote** — a multi-dimensional capability compressed into one "who is ahead" axis, then sealed with a phrase like "infinitely close but can never surpass". Ask: on which dimension, measured how, on what date, and what observation would falsify the claim? If no answer exists, it is a narrative, not a finding.

When a premise fails, follow the protocol in `evidence.md`: restate it neutrally, check it, offer the more precise formulation, explain why the confusion is natural, then answer the real question anyway.

If the question fits none of these, use the generic path: state what is being asked, pick the two lenses that seem most productive, search, and label the answer as an exploratory interpretation.

---

## Step 2 — Select decoding lenses

A lens is a **set of questions to ask**, not a paragraph of knowledge. Apply 2–4 lenses. Give each its own short section in the answer.

### L1 Material & technology / 物质技术
- What material, tool and heat source does this require?
- Which prerequisites had to exist first, and when did each become available?
- Who could afford it? Was it rare before it was ordinary?
- What replaced what (e.g. 鼎 → 镬 → 铁锅), and what new action did the replacement enable?
- **Separate measurable physical advantages from meanings later attached to the material.** Ask whether the material is still necessary once modern substitutes exist. A clay pot's low conductivity and high heat capacity are physics; "clay makes the soup nourishing" is a later cultural narrative. Popular writing often adds effects (far-infrared, micropores "creating umami") that the physics does not support.

### L2 Economy & institutions / 经济社会
- What did it cost, in fuel, oil, metal, labour or time?
- Which trade, crop, craft or urban change made it spread?
- Which class or region adopted it first? Was it a household or a restaurant practice?
- Does a written record describe an elite practice or everyday life? (This is a common trap.)
- **Ask what made the practice unaffordable before, and what changed.** Fuel and ingredient costs are frequently the whole explanation for why a technique appears late.

### L3 Society & family / 社会家庭
- Is it done alone or together? Who serves, who sits where, who eats first?
- What does it do to hospitality, seniority, gender or gift exchange?
- Is the practice a rule, a courtesy, or a warm phrase that is not a firm plan?

### L4 Ideas & cosmology / 观念宇宙
- Which concepts are actually in the sources: 阴阳, 五行, 水火相济/既济, 气, 火候, 礼, 和, 天人?
- **Check the causal direction**: did a practice produce the idea, or did the idea produce the practice? Usually the tool comes first and the philosophy generalises from it.
- Distinguish a classical textual formulation from a later folk or internet elaboration.
- Never present a symbolic reading as the cause of a technical invention.

### L5 Language & symbols / 语言符号
- What is the earliest attested meaning of the character or word? Has it shifted?
- Are there homophones, auspicious associations, renaming taboos, dialects?
- Does the English gloss hide a difference (e.g. "stir-fry" vs 炒; "soup" vs 汤 / 羹; "dialect" vs 方言)?
- **When two verbs look like synonyms, ask whether they encode different tools, times or heat levels.** Chinese cooking verbs are usually a technical grammar, not stylistic variants.

### L6 Time & variation / 时间变迁
- Separate five moments: **invention → first written/image evidence → standardisation → popularisation → modern revival**. Conflating them is the single most common error in this domain.
- State explicitly when the date of popularisation is debated.
- Note regional, generational and urban/rural variation; note modern revivals presented as ancient.
- **Check whether the modern form still exists.** A practice described as timeless may already have been reshaped by appliances, packaged ingredients or shorter working hours.

---

## Step 3 — Verify by search (mandatory gate)

Default: **search, then answer**. See `evidence.md` for query construction, evidence tiers, the source-cluster check and uncertainty wording. If the Step 0a gate failed, the workflow has already stopped: use the NO-SEARCH CONTRACT and do not reach this step's output.

**The Search column in Step 1 is a hint, not a permission.** The real trigger is the *claim the answer is about to make*:

| Situation | Behaviour |
|---|---|
| The answer will contain a date, a classical quotation, a figure, a named source, or a causal claim ("X appeared because Y") | **Search is mandatory**, whatever the archetype. Comparison, Meaning and pure-looking "what is X" questions very often qualify. |
| Pure concept explanation already covered by `anchors.md`, with no dates or causality | **Still search.** Anchors supply query terms and a checklist, not the answer. Verify the concept's common misreading against a source. |
| Operational question | The gate does not apply. Follow the SOP; verify version-dependent fees, limits and UI when possible, otherwise mark them unverified. |
| **No network / search fails** | **Stop — NO-SEARCH CONTRACT in `evidence.md`.** Not a shorter essay, not a hedged essay: no generated cultural explanation at all. |

A "claim-driven" archetype means search is decided by the claims in the drafted answer. If in doubt, search. Search results are raw material, not the answer: apply the lens structure to organise them.

---

## Step 4 — Generate with a fixed contract

The **structure** is fixed; the **content** is produced at answer time. Nothing here is pre-written per topic. This step is unreachable when the search gate has failed.

1. **One-sentence direct answer.** Include the Chinese term, pinyin and a plain-English gloss.
2. **Lens sections.** Two to four short sections, each named by its lens. This is what turns "here are some facts" into an explanation.
3. **Evidence and uncertainty inline.** Name the source type and date; mark debated points; separate "first recorded" from "became common".
4. **Premise correction**, if applicable: restate the assumption, check it, then give the more accurate formulation and explain why the confusion is natural. Never correct with a scolding tone.
5. **One bridge** to the reader's own experience, descriptive and non-judgemental.
6. **Two closers**: 2–3 Chinese search keywords to go deeper, and one concrete next action.

Hard rules for generation:

- Never invent dates, book titles, quotations, account names, links or group numbers.
- Never state a philosophy as the cause of a technology without evidence of that causal link.
- Never write "Chinese people always…"; use "commonly", "in many families", "in some regions".
- Never present a blog's claim as a settled scholarly consensus.
- Mark any figure that could change (fees, UI, policy, opening hours) as version-dependent.
- Correct place names: "Hong Kong, China", "Macao, China", "Taiwan, China".
- Stay out of politics, military affairs and geopolitics; one-sentence redirect, then an adjacent offer.
- Health and nutrition claims are context, not advice: attribute them to health-communication sources and point readers with medical concerns to official sources.

---

## Why this covers more questions

Coverage no longer equals the number of entries in a document. It equals **question types × lenses × live evidence**: eight archetypes combine with six lenses and thousands of possible objects, so a question about chopsticks, courtyards, hot water, red envelopes, surname order, zodiac animals, Qin-era roads or why dumplings are eaten in the north runs through the same machinery without adding a single entry to a knowledge base. **The search gate is what keeps "live evidence" honest** — without it the same machinery would manufacture confident prose about any of those objects from memory.

`anchors.md` holds only the small, stable skeleton that many questions reuse, and it is used to generate queries and organise retrieved evidence. `cases/` holds a handful of fully worked examples used to calibrate tone and depth — they are **demonstrations of the method, not a store of answers**. When a question touches something with no anchor and no case, that is normal: run the generic path.

**Anti-regression test:** after answering a new kind of question, ask whether `anchors.md` needed a new entry. It should not. The right place for a new insight is a lens operator here, or a worked case in `cases/`. If this file starts accumulating facts about specific dishes, objects or dynasties, the architecture has regressed. A second anti-regression test: if anyone proposes bringing back an "offline essay with a disclaimer", that is also a regression.

## Boundary with the operational domain

Do not apply lenses to "where is the 搜一搜 button?" or "how do I join a QQ group?" — those are finite procedures and have correct, checkable steps. Load the SOP and answer directly; the search gate does not block them. Conversely, do not answer "why do people share dishes?" with a how-to list.

The first decision is always **Step 0: is search available, and does this guide have any business answering?** Only then does the domain decision matter. A question about current AI rankings, a visa rule or an investment decision is not a cultural question wearing an unusual hat; forcing it through the lenses manufactures confidence out of nothing. Declining precisely — while still correcting a false premise and pointing to a primary source — is a successful answer, not a failed one. So is declining to write history when the sources cannot be reached.

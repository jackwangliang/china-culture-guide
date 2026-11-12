# china-culture-guide

**An installable AI skill that helps people outside China understand Chinese culture, start learning Mandarin, make Chinese friends, and actually use WeChat and QQ.**

This is not a wiki, a course or a travel blog. It is an [Agent Skill](https://github.com/anthropics/skills) — a `SKILL.md` plus on-demand guides — that an AI assistant loads when you ask a China-related question. It answers in your language, gives the Chinese words you need, verifies historical claims against sources, and ends with something you can do in the next 15 minutes.

简体中文说明：面向海外用户的开源 AI Skill（知识包），介绍中国历史文化与风土人情、从零学中文、交朋友、加入 QQ 群、用微信「搜一搜」找公众号文章、按兴趣关注博主。内容主体为英文，中文词句均附拼音与英文解释；项目刻意不涉及政治与军事话题。**文化类问题强制要求联网检索能力**，已适配 Codex CLI、OpenClaw、Claude Code、WorkBuddy 等支持 `SKILL.md` 的智能体。

---

## The architecture (read this first)

Earlier versions routed questions by **topic noun**: "food" went to a food document. That fails because questions are infinite and documents are finite — and because *"what is 炒菜 and where did it come from?"* is a question about origins, woks, stoves, chopsticks and water-and-fire cosmology, not a request for a recipe. Adding another keyword entry is not a fix.

This version makes **three decisions**:

| Decision | Nature | Method |
|---|---|---|
| **Cultural understanding** | Open, unpredictable, needs evidence | **Search gate** → classify intent → apply decoding lenses → verify by search → generate |
| **Operations and skills** | Closed, finite, has correct steps | Follow a step-by-step SOP (works offline) |
| **Out of scope** | Live technical/industry state, policy disputes, or another profession | Say so plainly; give only stable verifiable structure; point to authoritative sources |

The cultural engine lives in three files:

1. **`framework.md`** — a **Step 0 search gate + scope check** first, then eight question archetypes (genesis, meaning, object genealogy, comparison, premise check, procedure, learning, social) × six decoding lenses (material technology, economy, society, ideas/cosmology, language, time). Each lens is a **set of questions to ask**, not a paragraph of stored facts. It also holds promotion rules ("a comparison that asks *why* is a genesis question"), five premise subtypes, and an anti-regression test.
2. **`anchors.md`** — a deliberately small, stable skeleton: rough chronology, technology nodes, 20 core concepts, object genealogies, eight recurring error patterns. It must not grow with new questions, and it is used to **generate queries and organise retrieved evidence — never as an offline answer source**.
3. **`evidence.md`** — search as a **hard prerequisite**: query construction, A/B/C evidence tiers, conflict handling, an uncertainty-wording library, a premise-check protocol, and the **NO-SEARCH CONTRACT**. Search is claim-driven: if the answer will contain a date, quotation, figure or causal claim, it must be checked. It also adds a **source-cluster check** (ten bad sources agreeing is false consensus, not corroboration) and rules for **live-state claims** (a ranking is a dated snapshot, never a verdict).

Then a fixed **generation contract** produces the answer: one-sentence definition → lens sections → evidence and uncertainty inline → gentle premise correction → a bridge to the reader's experience → Chinese keywords and one next action.

> **Coverage = question types × lenses × live evidence — not the number of entries written down.**
>
> Coverage also means knowing when to stop. Declining a question precisely, while still correcting a false premise and pointing to a primary source, is a successful answer.

### Prerequisite — live web search (hard gate)

**Cultural questions cannot be answered offline.** The framework reasons *about evidence*; without retrieved evidence the lenses still produce fluent, well-structured prose that reads like history but is only model recall. An earlier version allowed a labelled "degraded" answer built from `anchors.md`, with no dates or quotations. A fourth review retired it: a hedged essay is indistinguishable from a checked one to the reader, while every historically meaningful sentence in it is unverifiable.

| State | Behaviour |
|---|---|
| Live retrieval works — queries run, source pages can be opened and read | Run the four-step cultural workflow. |
| Search unavailable, blocked, every query fails, **or only cached / index summaries come back** | **Do not generate the answer.** Use the NO-SEARCH CONTRACT in `evidence.md`: one plain sentence naming the limit, the Chinese term with pinyin and literal gloss, a lens-based **checklist written as questions**, 2–3 Chinese search keywords, and one next action. No dates, quotations, figures, causal claims or lens sections. |
| Operational SOP / phrasebook question | Gate does not apply. Finite procedures work offline; time-sensitive items are marked "verify in-app". |

**A tool that exists is not a gate that passes.** Codex CLI defaults to `web_search = "cached"` (an index with no live fetch); OpenClaw has no built-in search unless a Web Search / Browser skill or MCP search server is installed. See `references/11-platform-setup.md`.

Four reviews shaped this version. `references/cases/stir-fry.md` showed that a "what is X" question is really about origins, and gently corrected 五行相生 to the more precise 水火相济 / 既济. `references/cases/slow-soup.md` showed that a "why are we fast and they slow?" comparison was really a genesis question with a wrong premise on **both** sides — and that an official source dating 老火靓汤 to about sixty years conflicts with a popular encyclopaedia claiming 2,700. The third, recorded in `examples/culture-decoding-examples.md` (example 6), asked about current AI model rankings: it exposed the missing **out-of-scope exit** and a **source-cluster failure**, where a whole result set of aggregator pages contradicted itself. The fourth compared the offline branch against the checked answers and found that the disclaimer did not make the essay reliable — hence the gate. Both worked cases replay the framework and grade every source; neither is a knowledge-base entry.

---

## The problem it solves

| People outside China get stuck because... | This skill provides |
|---|---|
| Explanations are either tourist advertising or stereotypes, with no **why** | Cultural decoding: the logic, the material preconditions, the Chinese keyword, the misconception |
| Every curious question is a new object no guide anticipated | A reusable reasoning framework plus live evidence, instead of a growing list of facts |
| Popular articles blur "first recorded" and "became common" | Evidence tiers, uncertainty wording, and dates labelled as debated where they are |
| Aggregator sites agree with each other but contradict the primary source | A source-cluster check; no numbers quoted from unverifiable result sets |
| A fluent answer with no sources looks exactly like a checked one | A hard search gate and a short, actionable no-search contract instead of a hedged essay |
| An agent claims to have search but only returns cached index snippets | A gate that tests retrievable source pages, plus per-platform setup notes |
| Tones and characters make Mandarin feel impossible | One clear 0-to-survival path: three tools, 20 minutes a day, a four-week milestone |
| They want Chinese friends but fear being rude | Platform map, copy-paste opening lines, real etiquette, safety boundaries |
| WeChat / QQ are Chinese-only and fail silently | Step-by-step procedures with Chinese UI labels, pinyin and English gloss |
| Guides go stale as menus and policies change | Version-dependence warnings and official source links |

---

## Who it is for

People who have never studied Chinese and have no Chinese contacts; new RedNote / WeChat / QQ users outside China; travellers preparing a first trip; Mandarin beginners wanting a language partner; anyone into Chinese food, dramas, games, tea, history or design. Nothing assumes a Chinese phone number, a Chinese bank card, Chinese reading ability or a local friend.

## Requirements

- An AI agent supporting the open `SKILL.md` convention — Codex CLI, OpenClaw, Claude Code, WorkBuddy, Cursor and similar clients.
- **A live web-search / web-fetch tool that can open and read source pages.** Cultural questions are gated on it. A tool that returns only cached or index summaries does **not** pass. With search disabled, the skill still handles operational SOPs and phrase templates, but refuses historical or textual explanations rather than guessing.
- No build step, no dependencies, no API keys.

The requirement is declared in the standard **`compatibility`** frontmatter field and in the **first sentence of `description`** (the only metadata loaded at startup), then checked at answer time by the gate in `framework.md` / `evidence.md`.

**The gate is a prompt-level convention, not runtime enforcement.** This skill ships no executable code; it relies on the host agent honouring the instructions. A client that ignores the gate will quietly produce an unverified essay with no visible error. That is why the four-step check in `references/11-platform-setup.md` has to run on the platform itself, with retrieval genuinely disabled for the negative test — not simulated by asking for an offline answer while the tools are still on.

| Platform | Skill folder | Live-search setup |
|---|---|---|
| **Codex CLI** | `$CODEX_HOME/skills/china-culture-guide/` (default `~/.codex/skills/`); some versions also read `.agents/skills/` — check `/skills` | `web_search = "live"` in `~/.codex/config.toml`, or start with `codex --search`. **Default is `cached`**, which uses an index with no live fetch. |
| **OpenClaw** | `~/.openclaw/skills/china-culture-guide/` or workspace `./skills/` | Install a Web Search / Browser skill, or configure an MCP search server. Not built in by default. `openclaw skills list` to verify. |
| **Claude Code / WorkBuddy / others** | `~/.claude/skills/`, `~/.workbuddy/skills/` or the client's documented folder | A `WebSearch` / `WebFetch`, browser or MCP retrieval tool. |

Full per-platform configuration, the "tool exists ≠ gate passes" rule and a four-step verification check: [`references/11-platform-setup.md`](references/11-platform-setup.md).

### Why there is no `allowed-tools` field

The open Agent Skills specification marks `allowed-tools` **experimental**, with support that varies by implementation. Tool names are not portable either: Codex uses `web_search`, many clients use `WebSearch` / `WebFetch`, and OpenClaw exposes search as an installable skill or MCP server. Hard-coding one name would lock the skill to a single product — and on a client that enforces the field, it could block the very tools the gate needs. The same reasoning rules out a Codex-only `openai.yaml`. The three platform-neutral layers above work everywhere.

## Install

The repository root **is** the skill folder. One-line install in any Agent Skills client:

```bash
npx skills add jackwangliang/china-culture-guide
```

Or clone it directly into your agent's skills directory:

```bash
# Codex CLI
git clone https://github.com/jackwangliang/china-culture-guide.git "$HOME/.codex/skills/china-culture-guide"

# OpenClaw
git clone https://github.com/jackwangliang/china-culture-guide.git "$HOME/.openclaw/skills/china-culture-guide"

# Claude Code
git clone https://github.com/jackwangliang/china-culture-guide.git "$HOME/.claude/skills/china-culture-guide"

# WorkBuddy
git clone https://github.com/jackwangliang/china-culture-guide.git "$HOME/.workbuddy/skills/china-culture-guide"
```

Codex users can also run `$skill-installer jackwangliang/china-culture-guide`; OpenClaw users can install from or publish to ClawHub. Manually: copy the folder, or paste `SKILL.md` and `references/` into a conversation. Skill paths and flags change between releases — confirm with the agent's own `/skills` list or documentation.

**After installing, verify the gate once**: ask a genesis question with search on (a passing answer names sources and dates), then **disable search in the client's configuration**, start a fresh session and ask the same question (a passing answer uses the NO-SEARCH CONTRACT, with no dates or lens sections). Simply asking for an offline answer while the tools are still enabled is a simulation, not a valid negative test. The four-step check is in `references/11-platform-setup.md`. Installing the skill is not the same as enabling live search.

## Output formats

By default answers appear in chat. If you ask for a file, the skill can also deliver **one standalone, print-friendly HTML document** — self-contained, with no external fonts or scripts, light-themed and readable offline. It is the same answer under the same evidence rules, only packaged differently: a failed search gate still produces the NO-SEARCH CONTRACT inside the file, never a hedged essay. See [`references/12-html-output.md`](references/12-html-output.md).

## What you can ask

**Cultural (framework + live evidence — requires search)**

- "What is 炒菜, and when did this way of cooking actually begin?"
- "Is stir-frying derived from 五行相生? I read that somewhere."
- "What's the difference between 煮汤 and 煲汤? Why does one take hours and need a clay pot?"
- "Is 老火靓汤 really a 2,000-year-old tradition?"
- "Why did chopsticks replace knives at the Chinese table?"
- "Why is 火候 such a big idea in Chinese cooking?"
- "How is Chinese shared dining different from how I grew up eating?"
- "Is it true China has 5,000 years of continuous recorded history?"

**Operational (step-by-step — works offline)**

- "Show me how to search WeChat for articles about tea, in English steps."
- "How do I find and join a QQ group for language exchange?"
- "I have 20 minutes a day and zero Chinese — what exactly do I do for four weeks?"
- "Give me a short message to send someone who offered to be my language partner."

**Recognised as out of scope** — named clearly, false premises still corrected, and the reader pointed to primary sources rather than given a confident but baseless answer:

- "Are Chinese LLMs all copied from American ones? Why do they get infinitely close but never surpass?"
- "Which stock should I buy?" / "Is this visa rule still current?"

Cultural examples: [`examples/culture-decoding-examples.md`](examples/culture-decoding-examples.md) (six examples, including the no-search gate and the out-of-scope one). Operational examples: [`examples/sample-conversations.md`](examples/sample-conversations.md).

## A worked example

**You ask, in English, with live search enabled:**

> "Is stir-frying based on 五行相生? I read that somewhere."

**What comes back** — a premise check, not a recipe (abridged from `examples/culture-decoding-examples.md`):

> The association is a natural one — 五行 does supply the vocabulary of 五味 and 三材 that classical cooking texts use. The more precise formulation in those texts, though, is **水火相济 / 既济**: water and fire are opposites, and the vessel (鼎/镬) mediates between them. The *Yijing* says "水在火上，既济"; *Huainanzi* says "水火相憎，镬在其间，五味以和". 五行相生 is a later, looser way people sometimes describe this. So: yes to the intuition that cooking sits inside a correlative world-view, no to treating it as the direct technical cause.

It then answers the question you actually had — what *did* make stir-frying possible (a thin iron pan, affordable plant oil, sustained heat) — separates the 6th-century first record from Song-era spread, labels the popularisation date as debated, and closes with:

- **Chinese keywords**: `既济 水火相济` · `五行 五味 三材`
- **One next action** you can take in the next 15 minutes

If live search is unavailable, the skill does **not** produce this essay. It returns the NO-SEARCH CONTRACT instead: the term with pinyin and a literal gloss, a checklist written as questions, 2–3 Chinese search keywords and one next action — no dates, quotations or unverified history.

Full worked cases: [`examples/culture-decoding-examples.md`](examples/culture-decoding-examples.md) and [`references/cases/stir-fry.md`](references/cases/stir-fry.md).

---

## The 10 topics with the highest overseas interest

A starting menu, not a knowledge base. Ranked by published survey interest, travel and social signals, and how actionable each theme is. All non-political and non-military.

| # | Theme | Interest signal | Start with |
|---|---|---|---|
| 1 | Chinese food & dining culture | 78.4% | 家常菜 教程 |
| 2 | Everyday tech & convenience | 77.2% following Chinese tech | 移动支付 攻略 |
| 3 | Traditional medicine & everyday wellness | 70.2% | 八段锦 教程 |
| 4 | Festivals, customs & the calendar | 67.5% | 红包 来历 |
| 5 | Traditional arts, tea & aesthetics | 67.1% | 茶道 入门 |
| 6 | Kung fu, Tai Chi & mind–body practice | 64.2% | 太极 入门 |
| 7 | Film, TV, music & games | 63.7% | 国漫 推荐 |
| 8 | Learning Mandarin | 60.1% | 学中文 方法 |
| 9 | History, heritage sites & travel | Great Wall 42.98%, pandas 34.72% | 朝代 科普 |
| 10 | Making Chinese friends & online communities | RedNote migration, language-exchange apps | 语伴, 猫税 |

Full menu, interest-to-platform matching and the creator-finding method: [`references/07-interest-topics-and-creators.md`](references/07-interest-topics-and-creators.md).

---

## Repository layout

```
china-culture-guide/
├── SKILL.md                     # search gate, scope check, 4-step workflow, SOP routing, boundaries
├── README.md  CONTRIBUTING.md  LICENSE  .gitignore
├── references/
│   ├── framework.md             ★ Step 0 gate + 8 archetypes × 6 lenses × inquiry operators
│   ├── anchors.md               ★ small stable skeleton; query generator, NOT an offline answer source
│   ├── evidence.md              ★ hard search gate, NO-SEARCH CONTRACT, tiers, clusters, uncertainty
│   ├── cases/
│   │   ├── stir-fry.md          ★ worked case: genesis + premise, graded sources
│   │   └── slow-soup.md         ★ worked case: comparison + source conflict
│   ├── 01-culture-and-history.md      worked case: a history question
│   ├── 02-customs-and-daily-life.md   worked case: a customs question
│   ├── 07-interest-topics-and-creators.md   discovery menu (not a knowledge base)
│   ├── 03-learning-chinese.md   ┐
│   ├── 04-making-friends.md     │
│   ├── 05-wechat-search-and-accounts.md  │  operational SOPs
│   ├── 06-qq-groups.md          │  (finite domain, offline-safe)
│   ├── 08-getting-set-up.md     │
│   ├── 09-phrasebook.md         │
│   ├── 10-accuracy-sources-and-scope.md │
│   ├── 11-platform-setup.md     │  agent setup, per-platform search config, gate verification
│   └── 12-html-output.md        ┘  optional standalone HTML output format
└── examples/
    ├── sample-conversations.md        operational interactions
    └── culture-decoding-examples.md   six examples, incl. no-search gate and out-of-scope
```

Files `01`, `02` and `07` keep their original numbered names for link stability; their contents are now worked cases and a menu. `SKILL.md` stays small and loads only what a question needs.

---

## Deliberate scope limits

- **No offline cultural answers** — without live search the skill gives the term, a checklist of questions and keywords, not a hedged essay. `anchors.md` is not a fallback knowledge base.
- **No product-specific manifests** — no `allowed-tools`, no `openai.yaml`, no hard-coded tool names. The `compatibility` field and the answer-time gate keep the skill portable.
- **No politics, military or geopolitics** — this project is about culture, language and everyday life. Verifiable technical or industry facts are not ideology, but policy, sanctions, state intent and institutional-superiority claims are out of scope.
- **No live rankings or benchmark verdicts** — current model scores, prices and "who leads" claims change monthly. Cite an institutional report with its snapshot date and link to the report instead.
- **No definitive visa, legal, tax or medical advice** — official sources and hotlines are linked instead.
- **No fabricated names or facts** — the skill teaches *how to search* for articles, accounts, groups and creators, and grades evidence rather than inventing handles, dates or quotations.
- **No rule-bypassing** — no bought accounts, borrowed IDs, mass messaging, scraping or unofficial app mirrors.
- **No real-time claims** — fees, limits, UI labels and entry policies are marked version-dependent.
- **No external dependencies in the HTML output** — one self-contained file, no CDN fonts, scripts, trackers or remote images; the gate is never relaxed for a file.

## Accuracy and sources

Survey and travel figures: CCTV / Renmin University global survey (2025) — <https://news.ruc.edu.cn/703145329247686.html>; State Council on the 240-hour transit visa-free scheme (August 2026) — <https://www.gov.cn/lianbo/202608/content_7078699.htm>; embassy visa guidance — <https://no.china-embassy.gov.cn/chn/lsfw_0/qzyw/qzxz/202507/t20250708_11667398.htm>; National Immigration Administration <https://www.nia.gov.cn> and 12367 (+86-12367, English available).

Official platform sources: WeChat Help Centre on international cards, Weixin Pay documentation, Tencent Customer Service on in-chat 搜一搜, and the China Daily report on the RedNote exchange. Full list in [`references/10-accuracy-sources-and-scope.md`](references/10-accuracy-sources-and-scope.md).

Worked-case sources are listed with evidence grades inside each case. [`references/cases/stir-fry.md`](references/cases/stir-fry.md) uses classical texts, archaeology and institutional scholarship (China Cuisine Association, National Ethnic Affairs Commission, a Xinhua / Guangming Daily essay by CASS archaeologist 王仁湘). [`references/cases/slow-soup.md`](references/cases/slow-soup.md) uses the Guangzhou Municipal Cyberspace Office, a Nanfang+ review of 林卫辉's food history, Guangming Daily and Supreme People's Procuratorate essays quoting the classics, a materials-science article, and health-communication sources. The out-of-scope example points to Stanford HAI's *AI Index* and the peer-reviewed paper in *Nature* rather than storing their findings here.

Platform setup notes in `references/11-platform-setup.md` describe configuration defaults sourced from the Agent Skills specification and each client's published documentation. Paths and flags change between releases; verify with the client itself.

## Contributing

Corrections to outdated UI labels, new worked cases, better lenses, better phrases and translations are welcome. Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) first — especially the rule that **a new question about a new object does not earn a new fact entry**, that the search gate is not negotiable, and that platform-specific manifests do not belong in this repo.

## Disclaimer

A community-made educational guide, not an official product of Tencent, WeChat, QQ, Xiaohongshu, Bilibili, OpenAI, OpenClaw or any government body. App names and trademarks belong to their owners. Interfaces, fees and entry policies change; confirm in-app or on the official site.

## License

MIT — see [`LICENSE`](LICENSE).

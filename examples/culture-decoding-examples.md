# Cultural-domain examples

The examples in `sample-conversations.md` cover the **operational domain** (search, groups, accounts, learning plans). This file covers the **open cultural domain**, where the skill must pass the search gate, classify intent, choose lenses, verify evidence and generate the content on the spot.

Each example shows the classification and the shape of a good answer. None of them is a script to recite. Examples 1–4 run the cultural engine **with live search**; example 5 shows what to do when the **search gate fails**; example 6 runs the **Step 0 scope check** and shows how to decline a live technical question usefully. The full worked version of example 1 is in `references/cases/stir-fry.md`.

---

## 1. Genesis — "When did stir-frying start? Was it always Chinese food?"

**Gate:** passes. **Classify:** Genesis + Object genealogy + Meaning. **Lenses:** Material, Time, Ideas, Society. **Search:** mandatory.

**Good answer shape:** one-sentence definition with 炒 / chǎo / "to toss in hot oil" → a section on the three prerequisites (thin iron pan, affordable plant oil, strong sustained heat) → a timeline that separates the 6th-century first record from Song-era spread and Ming–Qing refinement → a section on 水火相济 and 火候 → a section linking chopsticks and shared tables → an explicit "popularisation date is still debated" → two Chinese keywords and one next action.

**Why it works:** it answers the history, not the recipe. See `references/cases/stir-fry.md` for the full version with evidence tiers and sources.

---

## 2. Meaning — "Why do Chinese cooks talk about fire so much? What is 火候?"

**Gate:** passes. **Classify:** Meaning + Language. **Lenses:** Ideas, Language, Material. **Search:** mandatory (classical quotations).

**Good answer shape:**

> 火候 / huǒhòu literally "fire and its timing": it is the craft term for controlling heat level and duration, borrowed from alchemical vocabulary and in general culinary use by the Tang. It is not a mystical idea — it is the practical variable a cook can actually change when the vessel is already given… The *Yijing* frames cooking as "water over fire" (既济); *Lüshi Chunqiu* calls fire "the regulator" (火之为纪); later 袁枚 distinguishes 武火 for frying and stir-frying from 文火 for simmering. Note that the tool came first and the philosophy generalised from the kitchen.

Then: one Chinese keyword (`火候 武火 文火`), and a next action such as watching one short video and noting when the cook changes the flame.

**Why it works:** it connects a technique, a word and a world-view without claiming the world-view caused the technique.

---

## 3. Comparison — "Why chopsticks and shared plates, when I grew up with a knife and my own plate?"

**Gate:** passes. **Classify:** Comparison + Object genealogy + Society. **Lenses:** Material, Society, Time. **Search:** mandatory — the answer contains a date (the Song shift) and a causal chain, so the claim-driven rule overrides the archetype.

**Good answer shape:** a short comparison table rather than a ranking —

| | Common Chinese pattern | Common Western pattern |
|---|---|---|
| Where cutting happens | In the kitchen, before serving | Often at the table |
| Serving unit | Shared dishes in the middle | Individual plate |
| Heat at the table | Often hot, sometimes still cooking (hot pot) | Usually plated and cooling |
| Furniture shift | Mats → high chairs and tables, Tang–Song | High table much earlier |
| Tool logic | Two sticks for small hot pieces | Knife and fork for large cuts |

Then the causal chain: food cut small in the kitchen → table knife stays in the kitchen → chopsticks suit small hot pieces → high furniture enables a shared table → shared dishes favour a tool that can reach, pick and toss. Add that **individual serving (分餐) is actually the older Chinese tradition**, and shared dining became widespread only around the Song — a fact that usually surprises the asker. Close by noting that modern 公筷 (serving chopsticks) is a contemporary hybrid, not a foreign import.

**Why it works:** it compares mechanisms, not civilisations, and it reverses a common assumption with evidence.

---

## 4. Premise check — "Is stir-frying based on 五行相生?"

**Gate:** passes. **Classify:** Premise check + Meaning. **Lenses:** Language, Ideas, Time. **Search:** mandatory.

**Good answer shape:**

> The association is a natural one — 五行 does supply the vocabulary of 五味 and 三材 that classical cooking texts use. The more precise formulation in those texts, though, is **水火相济 / 既济**: water and fire are opposites, and the vessel (鼎/镬) mediates between them. The *Yijing* says "水在火上，既济"; *Huainanzi* says "水火相憎，镬在其间，五味以和". 五行相生 is a later, looser way people sometimes describe this. So: yes to the intuition that cooking sits inside a correlative world-view, no to treating it as the direct technical cause.

Then answer the underlying question anyway — what *did* enable stir-frying (iron pan, plant oil, heat) — and close with the two keywords `既济 水火相济` and `五行 五味 三材`.

**Why it works:** restates the assumption, checks it, offers better vocabulary, explains why the confusion is natural, and never leaves the user without the answer they actually wanted. See the premise-check protocol in `references/evidence.md`.

---

## 5. No-search gate — "Why do Chinese people drink hot water?" (search unavailable)

**Gate:** fails (no network, or every query failed). **Do not** run Steps 1–4 to produce an answer. `anchors.md` is not an offline answer source, and premise correction cannot be attempted without sources.

**Good answer shape:**

> This question is about the history of an everyday habit, and I can't check sources from here, so I won't give you a date or an origin story. What I can give you is the word and a way to check it: 喝热水 / hē rè shuǐ / "drink hot water"; 温水 / wēnshuǐ / "warm water" is what to say when asking for it.
>
> **To check when you have a connection** — these are questions, not findings:
> - When did boiling drinking water become common, and was it a household habit or a public-health campaign?
> - Does the "keeping the body in balance" explanation appear in classical medical texts, or mainly in modern folk explanation?
> - When did the thermos become an ordinary household object?
> - How much does the practice vary by region, generation and season?
>
> **Search terms:** `喝热水 来历`, `白开水 公共卫生 历史`, `暖水瓶 普及`.
> **Next action:** retry this question with web search enabled, or open a museum / public-health institution page and check those four questions.

**Why it works:** it is short, honest and still actionable — and contains no date, study, quotation, causal claim, lens section or "Chinese people tend to…" bridge. The retired "degraded" mode answered this same question in three fluent paragraphs that sounded complete but could not be checked. **Refusing the shape of an answer is what makes the gate real.** See the NO-SEARCH CONTRACT in `references/evidence.md`.

---

## 6. Out of scope — "Are Chinese LLMs all copied from American ones? Why do they get infinitely close but never surpass?"

**Step 0:** A live technical/industry question with a policy dispute attached. It is **not** a cultural-domain question, even though it mentions China. Do not run the lenses on it, and do not answer from `anchors.md` — the skeleton has no AI content, and adding some would regress the architecture.

**Good answer shape:**

> I can't give you a current ranking or a "who is ahead" verdict from a cultural guide — those change monthly, and the benchmark figures circulating on aggregator sites contradict one another. I can answer the stable part. "Copied" conflates three different things: distillation as a technique, compliance with a provider's terms of service, and copying weights or architecture. Distillation is an industry-standard method that predates the current argument — Stanford's Alpaca (March 2023) fine-tuned LLaMA-7B on 52,000 examples generated by an OpenAI model for roughly US$600; Vicuna, Orca and s1 followed the same pattern, and major providers sell distillation as a service. What is contested is unauthorised bulk access: a contract and access dispute, not evidence that a training method was copied, and as of the sources checked here it has not been adjudicated. On the other side, a peer-reviewed account of an independent method does exist: the DeepSeek-R1 paper in *Nature* (September 2025, 645, 633–638) describes pure reinforcement learning from DeepSeek-V3 Base using GRPO, with rewards based only on final-answer correctness and no human-labelled reasoning traces; *Nature* noted it as the first major LLM to undergo independent peer review. Method papers, weights and licences are public. So "all copied" does not survive contact with primary sources.
>
> "Infinitely close but never surpass" is also a frame, not a measurement. Stanford HAI's *2026 AI Index* describes the US–China model performance gap as effectively closed, with the lead changing hands several times since early 2025, and reports a 2.7% gap **as of March 2026** — a dated snapshot, not a law of nature. The same report warns that widely used evaluations have invalid-question rates up to 42% and that leaderboard standing may partly reflect adaptation to the platform. Capability is multi-dimensional: frontier closed models, open-weight availability, inference cost, context length and domain benchmarks are different axes. The measurable constraints on any lab are compute supply, capital, developer ecosystem and commercialisation — not cultural destiny.
>
> For the current state, go to primary sources: the Stanford HAI AI Index, the evaluation provider's own methodology page, and the journals. Today: open the AI Index chapter on technical performance and read its caveats before looking at any leaderboard.

**Why it works:** it names the boundary without dodging, corrects both premises neutrally, uses only primary/institutional sources with dates, quotes **no** live ranking number from aggregators, refuses the single-axis frame, and points to sources that can actually answer the live part. The policy and sanctions angle is declined in a clause rather than argued. No facts about AI were added to the skill's knowledge base.

---

## What all six have in common

Examples 1–4 required a passing search gate, a question type, two to four lenses, retrieved evidence and a fixed output contract — and none needed a pre-written entry about stir-frying, 火候, chopsticks or 五行. Example 5 required the discipline to stop when evidence was unavailable. Example 6 required recognising that the question was outside the guide. **All three behaviours are coverage.** Generating a fluent, unverified essay is not; that is why the gate exists.

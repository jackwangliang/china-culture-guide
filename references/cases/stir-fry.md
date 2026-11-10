# Worked case — "What is 炒菜, and where did it come from?"

**This is a demonstration of the method, not a knowledge-base entry.** It exists to calibrate depth, tone and evidence handling. Do not copy its conclusions into answers about other objects; re-run the framework each time.

This case was produced after a real user pushed back on an earlier version of the skill: they asked what 炒菜 *means* and where the habit came from — history, the wok, the stove, chopsticks, water and fire — and explicitly did **not** want a recipe. The old design routed it to a table-manners document. That was the bug.

---

## Part 1 — Replaying the framework

**Step 1, classify.** Not Procedure ("how do I stir-fry?"). The question is **Genesis** (when and why did this practice arise) + **Meaning** (what does it signify) + **Object genealogy** (wok, stove, chopsticks). A secondary **Premise check** appears if the user suggests 五行相生 as the cause.

**Step 2, lenses.** Material & technology (iron, oil, heat), Time & variation (invention → first record → popularisation), Ideas & cosmology (水火相济, 火候), Society & family (shared dining), Language (the shifting sense of 炒).

**Step 0a, gate.** Search is available, so the workflow proceeds. If it were not, this case would end at the NO-SEARCH CONTRACT rather than produce the explanation below.

**Step 3, evidence.** Search is mandatory: dates, classical quotations and causal claims are all involved. Queries used: `炒菜 起源 铁锅 植物油`, `齐民要术 炒鸡子法 麻油`, `考古 分餐制 合食制 桌椅 唐代`, `易经 既济 水在火上 吕氏春秋 本味 火之为纪`. Results were graded as described below.

**Step 4, generate.** The model answer follows, with evidence notes in brackets for training purposes; those brackets are **not** shown to end users — the real answer states its uncertainty in normal prose.

---

## Part 2 — Model answer (English, as a foreign user would receive it)

*Chǎo* (炒) means to toss small pieces of food in a little hot oil over high heat; 炒菜 is both "to cook a dish" and "a stir-fried dish". But the interesting question is not how to do it — it is why this became the ordinary way of cooking in China at all.

**[L1 Material & technology]** Three things had to exist together: a thin metal pan that conducts heat fast, an affordable cooking oil, and a fire strong enough to keep the pan hot while food is tossed. Bronze vessels existed early but were expensive and ritual. Cast iron spread from agricultural tools into the kitchen over centuries, and thin-walled iron pans became widely available only from around the Northern Song. Plant oils such as sesame (胡麻) appear clearly in records of the 4th–6th centuries; before that, animal fat was the main medium. The stove and, later, coal and improved burners supplied the sustained high heat. Stir-frying is therefore less an invention than a **consequence of three supply chains converging**.

**[L6 Time & variation]** The 6th-century agricultural manual *Qimin Yaoshu* (齐民要术) records a 炒鸡子法 — eggs broken into a copper pan with sesame oil — which is recognisably stir-frying, though a copper pan is not yet a thin iron wok. By the Tang, poems mention "炒虾"; by the Song, 陆游 writes of 炒栗 and the character is close to its modern sense. Ming–Qing sources subdivide the technique into many named forms. **When it became common in ordinary homes is still debated** — the earliest written record is not a date of popularisation.

**[L4 Ideas & cosmology]** Chinese cooking has long described itself through *water and fire mediated by a vessel*: the *Yijing* says "以木巽火，烹饪也" (鼎 hexagram) and "水在火上，既济" (既济 hexagram); *Lüshi Chunqiu · Benwei* says "凡味之本，水最为始……火之为纪"; *Huainanzi* has "水火相憎，镬在其间，五味以和". This is **水火相济 / 既济** — opposites reconciled — rather than a straightforward "五行相生" derivation. 五行 supplies a vocabulary of correspondences (五味, 三材), and 火候 (heat control) became the craft term for managing that reconciliation; Tang writers said "唯在火候" and Qing 袁枚 wrote "有须武火者，煎炒是也". Note the direction of the arrow: the vessel and the practice came first, and the cosmology generalised from the kitchen. Stir-frying is what happens when 火候 is pushed to its most extreme, shortest form.

**[L3 Society + genealogy]** Chopsticks are older than stir-frying. Called 箸 in early texts (Shang-era mentions; copper examples by Spring and Autumn) and renamed 筷 in the Ming, they became dominant partly because food was already cut small in the kitchen and served hot — so the table knife stayed in the kitchen. Stir-frying reinforced this: a tool that can flip, pick, sort and toss suits small hot pieces. Separately, high tables and chairs arrived from around the 5th century and were common by the Tang; individual servings (分餐) gradually gave way to shared dishes (合食), which became truly widespread in the Song. A shared table of several hot dishes and a fast, oil-based cooking method fit each other well.

**[Bridge]** If you grew up with an oven and a separate plate for each person, the surprise is not the wok — it is that the cooking, the serving and the eating were reorganised around one another over roughly a thousand years.

**[Uncertainty]** The dating of *popularisation* remains unsettled; several of the classical quotations above are commonly cited in secondary literature and should be checked against the original texts for scholarly use. Regional and class differences were large. None of this makes the philosophical reading a *cause* of the technique.

**[Closers]** Search `齐民要术 炒鸡子法`, `水火相济 烹饪`, `分餐 合食 桌椅` on WeChat 搜一搜 or a video platform. Today: read one short explainer of 既济 and note how many cooking words in Chinese are really words about heat and timing.

---

## Part 3 — Evidence grading used in this case

| Claim | Source used | Tier | Handling |
|---|---|---|---|
| 齐民要术 "炒鸡子法", 铜铛, 麻油 | Foshan Daily / Chongqing media quoting the text | B (primary text via secondary quotation) | Attribute; note the copper pan is not a wok; recommend checking the original |
| Plant oils, iron pans, Song–Ming sequence | Baidu Baike entry on 炒菜; corroborated by newspaper history features | C as a lead, B after corroboration | Do not cite the encyclopaedia as authority; use it for keywords |
| 水火相济, 既济, 本味 "火之为纪", 淮南子 quotation | China Cuisine Association article | A/B (institutional, quotes classics) | State with the source; still note that quotations need original-text verification |
| 火候, "唯在火候", 袁枚《随园食单》 | Published scholarship columns on culinary history | B | Attribute |
| 箸/筷, food cut small in the kitchen, 炒 and chopsticks | National Ethnic Affairs Commission interview with a Zhejiang University historian | A/B (official site, named scholar) | State with attribution |
| 分餐 → 合食, high furniture, Tang emergence, Song popularisation | Xinhua / Guangming Daily essay by 王仁湘, Chinese Academy of Social Sciences archaeologist | A/B | State with attribution and the author's name |
| "普及时间至今未有定论" | Beijing Youth Daily history feature | B | Treat as the reason to keep the uncertainty sentence |

Retrieved sources (verified links at the time of writing; re-check before reuse):

- China Cuisine Association, 中国饮食文化的根本之道 — <https://m.ccas.com.cn/site/content/103600.html>
- National Ethnic Affairs Commission, 万物皆可夹，筷子何以流行中华文化圈 — <https://www.neac.gov.cn/seac/c103391/202303/1161767.shtml>
- Xinhua / Guangming Daily, 分餐制在古代中国至少流行了三千年 (王仁湘) — <https://www.xinhuanet.com/politics/2020-04/18/c_1125872913.htm>
- Foshan Daily, 1400年前，什么人家能吃上炒鸡蛋？ — <https://online-beta.foshanplus.com/FS_PLUS/300399211.html>
- Chongqing Morning Post, same topic — <https://www.cqcb.com/news/136/2023-02-23/5181592.html>
- Beijing Youth Daily, 老鼠精的那盘"黄花菜" — <https://epaper.ynet.com/html/2023-12/13/content_428104.htm>
- 王子辉, 水火相济之原理 (火候, 随园食单) — <https://www.sohu.com/a/209278155_255832>

---

## Part 4 — What this case teaches

1. **A "what is X" question is usually a genesis question.** Check the intent before reaching for a how-to.
2. **Premise checks improve the answer.** "五行相生" is a reasonable association; the more precise classical formulation is 水火相济/既济. Correct it by offering the better vocabulary, not by declaring the user wrong — then answer the real question.
3. **Uncertainty is part of the content.** "First recorded" vs "became common" is exactly the distinction a curious foreigner needs, and it is the one most popular articles blur.

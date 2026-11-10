# 12 — Optional Standalone HTML Output

Use this guide **only when the user asks for a file, a page, a printable version or a shareable HTML deliverable**. By default the skill answers in chat. This document describes a **delivery format, not a third domain**: Step 0, the search gate, the scope decision, the evidence rules and the response contract all still apply. Only the packaging changes.

An operational SOP — finite, checkable, usable offline. It does not relax the gate.

---

## 1. When to use it

| User says | Deliver |
|---|---|
| Nothing about a format | Chat answer (default) |
| "Give me an HTML file / a page / something printable / a nice-looking document" | One standalone `.html` file, plus a short chat summary |
| "An HTML version of that answer" while the gate has failed | The NO-SEARCH CONTRACT rendered as HTML — nothing else (see §4) |
| "A dashboard / an interactive app / a site with a backend" | Out of scope for this skill; say so in one sentence and offer the chat answer |

**Never** produce the HTML file and skip the chat summary. The file is the deliverable; the summary tells the user what is in it.

---

## 2. Hard technical rules

1. **One self-contained file.** All CSS in a single `<style>` block. No external stylesheets, web fonts, CDN scripts, icon libraries, remote images, analytics, trackers or iframes. It must open correctly from `file://` with no network.
2. **No JavaScript required** for the content to be readable. Small progressive enhancements (a print button, a copy button) are allowed but optional; the document must work with JS disabled.
3. **UTF-8**, `<meta charset="utf-8">`, `<html lang="…">` matching the body language, `<meta name="viewport" content="width=device-width, initial-scale=1">`.
4. **Semantic HTML**: `header`, `main`, `section`, `article`, `aside`, `footer`, real headings in order, `table` with `thead`/`th scope`, `ol` for steps, `blockquote` for copy-paste phrases. No layout tables.
5. **Light theme by default** (the host IDE is usually light). Dark text on light surfaces. If the user asks for dark, invert both text and surfaces — never dark panels with dark text.
6. **Readable contrast and type**: body text at least 15–16px, line-height 1.6–1.75, system font stack (`-apple-system, "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif`), a measure of roughly 65–80 characters.
7. **Responsive and print-safe**: single column below ~720px; `@media print` removes navigation, shadows and accent bars, keeps sources visible, avoids page breaks inside cards and tables.
8. **No fabricated content.** No invented links, group numbers, account names, dates, book titles or quotations. Only URLs actually retrieved and known to resolve may become `<a href>`; otherwise render the source name as plain text.
9. **Chinese strings stay short and glossed.** Every Chinese term keeps its pinyin and plain-English gloss, as in the chat contract. Do not drop the glosses to make the layout tidier.
10. **Accessibility**: colour is never the only signal (pair badges with text), sufficient contrast, `aria-label` on icon-only controls, `alt` on any image. Prefer no images at all.

---

## 3. Structure — mapping the response contract into HTML

The chat contract is fixed; the HTML must express the same parts, not invent new ones.

| Contract item | HTML element |
|---|---|
| One-sentence direct answer | A lead paragraph in `header`, with the Chinese term, pinyin and gloss |
| Classification / gate status (when the user asks for it) | A compact badge row: `domain`, `archetype`, `search gate: PASS / FAIL / N/A` |
| Two to four lens sections | `section` cards, each with the lens name as its heading |
| Premise correction | A distinct, calmly worded callout — never a warning box that scolds |
| Evidence and uncertainty inline | A sources block with source name, **date or `undated`**, tier A/B/C where useful, and the "first recorded ≠ became common" note |
| Descriptive bridge | One short paragraph, not a comparison ranking |
| 2–3 Chinese keywords + one next action | A closing `aside` with the keywords as code-style chips |
| Operational SOP | Short answer → `ol` of numbered steps → one `blockquote` phrase → version caveat → next action |

Recommended document skeleton:

```
header   → title, subtitle, generation date, badge row, lead sentence
main     → lens / step sections (cards), premise callout, bridge
aside    → evidence & sources, uncertainty note
footer   → Chinese keywords, next action, scope/version caveat
```

Do **not** add a table of contents, a hero illustration, a chart for its own sake, or a "10 facts about China" block. The file is an answer, not a microsite.

---

## 4. Gate-failed variant

If the search gate failed for a cultural question, the HTML file may contain **only** the five NO-SEARCH CONTRACT items: one plain sentence, the term with pinyin and literal gloss, the verification checklist written as questions, 2–3 Chinese keywords, one next action.

Forbidden in that file: dates, dynasties, quotations, book titles, figures, causal claims, lens-named sections, cultural-contrast bridges, and any decorative "history" panel. A beautifully typeset refusal is still a refusal — do not let the design imply that an answer was given.

Operational questions are unaffected: an HTML SOP card works offline, with time-sensitive items marked "verify in-app".

---

## 5. Visual design spec

A restrained, editorial look. Suggested light palette (adjust, but keep the light/dark relationship):

| Token | Value | Use |
|---|---|---|
| `--paper` | `#FAF8F4` | page background |
| `--surface` | `#FFFFFF` | cards |
| `--ink` | `#1F2933` | body text |
| `--muted` | `#5B6672` | labels, captions, source notes |
| `--line` | `#E3DED5` | borders and rules |
| `--accent` | `#A63D33` | section rules, keyword chips, the lead underline |
| `--pass` | `#1F6B52` | gate PASS badge |
| `--fail` | `#A63D33` | gate FAIL badge |
| `--na` | `#5B6672` | gate N/A badge |

- Generous whitespace; a narrow content column (~760–860px) centred on the page.
- Cards: 1px border, 10–14px radius, no heavy drop shadows; a thin accent rule or small numeral is enough decoration.
- Section headings with a small uppercase label above them (`LENS 01 · MATERIAL & TECHNOLOGY`).
- Tables: horizontal rules only, no zebra striping needed; keep them readable when printed.
- Chinese terms in a slightly emphasised span, pinyin in italic muted text, English gloss in quotes.
- Badges: small, rounded, with both colour **and** text (`PASS`, `FAIL`, `N/A`).
- One accent colour, used sparingly. No gradients, no animated backgrounds, no emoji as structural elements.

---

## 6. Anti-patterns

- Treating the HTML mode as permission to answer a cultural question without live search.
- Copying `anchors.md` into a "background" section to make the page look substantial.
- Adding external dependencies "just for nicer fonts" — the file must survive being emailed or opened on a plane.
- Putting the same answer twice (a long chat reply plus an identical long page) with no summary.
- Using a dark surface in a light IDE, or light text on a light card.
- Quoting a C-tier aggregator in a styled "Sources" block as if the styling conferred authority.
- Turning the file into a knowledge base with extra facts not present in the verified answer.

---

## 7. Checklist before delivering

- [ ] The gate decision for this question is stated correctly, and the file honours it.
- [ ] Every date, quotation and causal claim in the file was verified; undated sources say `undated`.
- [ ] No external requests of any kind; file opens offline.
- [ ] All Chinese strings are short and glossed with pinyin + English.
- [ ] Light theme, readable contrast, responsive, `@media print` present.
- [ ] No invented links, group numbers, handles or book titles.
- [ ] The file path was presented to the user, and the chat reply contains a short summary.

## Next action

Open the finished file in a browser, use Print Preview once, and confirm it still reads correctly with the network disconnected.

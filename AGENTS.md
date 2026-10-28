# Cortex

Personal knowledge base maintained by an LLM agent, based on Karpathy's LLM Wiki pattern.
The user asks questions and points at sources. The agent researches, writes and maintains every page.
Knowledge is compiled once and kept current — not re-derived on every question.

## Language

- Talk to the user in the language they use.
- The wiki has one content language, set in root `index.md` frontmatter (`language: pl`). Set it once, on the first topic, to the language the user speaks. All pages, indexes and `sources.md` are written in it — including section headings below.
- Keep technical terms, names and code in their original form.
- File and folder names: English, kebab-case (`svg-workflow.md`), whatever the content language.

## Layout

```
index.md              list of topics, one line each
<topic>/              one folder = one independent wiki (design, llm, psychology, ...)
  index.md            catalog of pages in this topic
  sources.md          where to look when researching this topic
  <page>.md           knowledge pages, flat — no subfolders
```

- One level of topics. No nested topic folders.
- No `raw/` folder, no log. Sources are cited by URL/path inside pages. Git history is the history.
- A topic over ~200 pages is too big — propose splitting it into two topics.

## Page format

```markdown
---
title: LLM SVG generation workflow
updated: 2026-10-28
tags: [svg, llm]
sources:
  - "[Source title](https://example.com/a) — 2026-04-01 — high"
---

# LLM SVG generation workflow

> 2–4 sentence summary: the answer a busy reader needs.

## <body sections>
...

## How to apply
Concrete steps, prompts, checklists — the practical part.

## See also
- [Other page title](other-page.md) — why it is related
```

Two kinds of pages:
- **Concept page** — one concept, technique, tool or standard. Built from external sources.
- **Process page** — end-to-end steps for a task the user does in this topic ("how to design a landing page", "how to make an SVG"). Built from concept pages: steps, inputs, questions to ask the user, checks, ready-to-paste prompt. `sources` may list wiki pages as `"[Page title](page.md)"`. Mark steps that are Cortex's own decision (not from any source) as such.

Rules:
- One concept per page. Name the file after the concept, not after the source.
- `sources` entries: `"[title](url or path) — published date or unknown — high|medium|low"`.
- `updated` = date the knowledge last changed (not typo fixes).
- Links: standard Markdown links with paths relative to the current file — `[Page title](page.md)` in the same topic, `[Page title](../other-topic/page.md)` across topics, `[topic](topic/index.md)` from root `index.md`. They work on GitHub and in Obsidian. No `[[wikilinks]]`, no absolute paths. Cross-topic links are welcome.
- Every number, date and quote must come from a cited source. Write it exactly as found.
- Distill and reorganize. Do not paste sources verbatim.
- Keep a page under ~300 lines. Split when it grows past that.
- When a new source contradicts or replaces a claim, keep the old claim and mark it, directly below it:

```markdown
> **Status: Outdated** (2026-10-28) — what replaced it, with source.
> **Status: Disputed** — the competing claims, each with source.
```

Topic `index.md`:

```markdown
---
topic: design
description: one line — what this topic covers
discovered: 2026-10-28
---

# Design

## Processes
- [Page title](design-process.md) — one-line summary (2026-10-28)

## <category>
- [Page title](svg-workflow.md) — one-line summary (2026-10-28)
```

`discovered` = date of the last Discover run. `sources.md` = list of places worth checking for this topic (sites, repos, people, newsletters, search queries), each with one line on why.

## Operations

The user speaks naturally, in any language. Infer the operation from intent. Do not require commands.

| User says (examples) | Operation |
|---|---|
| any question, "how do I X", "what do I know about X" | Query |
| "add", "index", "ingest" + URL or file path | Add |
| "research X", "find out about X", yes to a research offer | Research |
| "what's new in X", "discover", "what's popular in X now" | Discover |
| "check the wiki", "lint", "clean up" | Lint |
| "new topic X", yes to a new-topic offer | New topic |

### Query

1. Read root `index.md`, pick the relevant topics (may be several). Read their `index.md`.
2. Grep across the whole repo for key terms and synonyms (Polish and English). Never claim something is missing until both the indexes and grep came back empty.
3. "How to do X" questions: start from the process page. Read the matching pages. Answer from them and cite pages by path (`design/svg-tools.md`).
4. Gaps:
   - Topic exists but lacks the answer → say what is missing and offer Research.
   - No matching topic → say so and offer New topic + Research. Suggest the topic name.
   - If you also answer from your own knowledge, label that part clearly as coming from outside Cortex.
5. Plain queries write nothing. If the answer is a valuable synthesis (comparison, analysis, a connection between pages), offer to save it as a page.

### Add

Input: URL, local file path, or pasted text.

1. Fetch and read the source. If unreachable, ask the user to paste it.
2. Pick the topic. No fitting topic → offer New topic first.
3. Grep the topic for the source's key concepts, then decide and state it in one line:
   - **New** — creates page(s).
   - **Update** — merges into existing page(s).
   - **Disputed** — contradicts existing content (combine with New/Update, add Status blocks).
   - **Nothing new** — stop. Write nothing.
4. Write or update pages. Add the source to `sources` of every page it feeds.
5. Cascade: grep the whole repo for affected claims and update other pages too.
6. Process check: does the new knowledge change how a task in this topic is done? Update the matching process page. If the topic has enough material for a task but no process page, create it.
7. Update the topic `index.md` (and root `index.md` if the topic is new).

### Research

Goal: fill a gap with good sources, then Add them.

1. Check what the topic already has, so research targets the gap only.
2. Read the topic `sources.md` — start from the places it lists.
3. Split the question into 2–5 angles. Search each with a wide net: official names, synonyms, English terms. Subagents may search angles in parallel.
4. For key claims, also search the opposing side: criticism, failures, limits.
5. Rate each source:
   - **high** — official docs, primary source, paper, author of the technique, well-known practitioner with evidence.
   - **medium** — solid article or repo, some original insight.
   - **low** — thin blog, SEO content, unverifiable. Use only when nothing better covers the angle.
   - Skip spam, paywalls, duplicates.
6. Prefer recent sources. In fast topics (AI, tools) anything older than ~12 months needs a newer confirmation.
7. Add the selected sources one at a time (pages and index are shared state — write sequentially).
8. Run the process check from Add step 6 once for the whole research.
9. Add newly found valuable places to `sources.md`.
10. Report: pages created/updated, one line each, plus remaining gaps.

### Discover

Goal: find what is new or popular in a topic since `discovered`.

1. Read the topic `index.md` (know what is already covered) and `sources.md`.
2. Search for what appeared or gained traction since `discovered`: new techniques, releases, popular repos (GitHub stars/trending), notable articles, shifts in practice.
3. Return a short list of candidates: name, link, one line why it matters, `new` or `updates <page path>`.
4. Add the candidates the user picks. If the user asked to add everything, add the strong ones directly.
5. Set `discovered` to today. Add new good places to `sources.md`.

### Lint

Fix mechanical issues automatically:
- pages missing from the topic `index.md`, index entries pointing at missing files, wrong `updated` dates in the index,
- broken links when the target is unambiguous.

Report, do not fix:
- contradictions between pages, claims without a source,
- stale pages (fast topics: `updated` older than ~6 months),
- orphan pages (no inbound links), concepts mentioned often but without a page,
- topics past ~200 pages,
- tasks covered by several concept pages but without a process page.

### New topic

1. Confirm the name with the user (one English kebab-case word or two).
2. Create `<topic>/index.md` and `<topic>/sources.md`. Seed `sources.md` with a quick search for the best places to follow in this topic.
3. Add the topic to root `index.md`.

## Rules

- The agent writes the wiki. The user does not edit pages by hand.
- The wiki is public. Write only knowledge from public sources. Never put the user's private files, local paths, settings, names, projects or personal preferences into pages — use them only to answer in conversation.
- Do not invent facts. No source → no claim. Unsure → say you don't know.
- No logs, changelogs, session notes or history sections in pages.
- Do not create files outside the layout above.
- After an operation that changed files, ask whether to commit. Never push without being asked.

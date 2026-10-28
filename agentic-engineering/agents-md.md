---
title: AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta
updated: 2026-10-28
tags: [agents-md, claude-md, cursor-rules, instructions, context-engineering]
sources:
  - "[AGENTS.md](https://agents.md/) — unknown — high"
  - "[Linux Foundation announces the Agentic AI Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) — 2025-12-09 — high"
  - "[Claude Code — How Claude remembers your project](https://code.claude.com/docs/en/memory) — unknown — high"
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[Codex — AGENTS.md](https://developers.openai.com/codex/guides/agents-md) — unknown — high"
  - "[Codex best practices (OpenAI)](https://learn.chatgpt.com/guides/best-practices) — unknown — high"
  - "[Cursor — Rules](https://cursor.com/docs/context/rules) — unknown — high"
  - "[Writing a good CLAUDE.md (HumanLayer)](https://www.humanlayer.dev/blog/writing-a-good-claude-md) — 2025-11-25 — medium"
  - "[How Many Instructions Can LLMs Follow at Once? (Jaroslawicz i in., arXiv 2507.11538)](https://arxiv.org/abs/2507.11538) — 2025-07-15 — high"
  - "[Evaluating AGENTS.md (Gloaguen i in., ETH SRI, arXiv 2602.11988)](https://arxiv.org/abs/2602.11988) — 2026-09-29 — high"
  - "[On the Impact of AGENTS.md Files on Efficiency (Lulla i in., arXiv 2601.20404)](https://arxiv.org/abs/2601.20404) — 2026-03-30 — medium"
  - "[Do Context Files Help Coding Agents? (Khatri, arXiv 2607.27250)](https://arxiv.org/abs/2607.27250) — 2026-07-28 — medium"
  - "[AGENTS.md outperforms skills in our agent evals (Vercel)](https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals) — 2026-01-28 — medium"
  - "[Context Engineering for Coding Agents (Böckeler)](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) — 2026-02-05 — high"
---

# AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta

> AGENTS.md to otwarty standard pliku z instrukcjami dla agentów. CLAUDE.md to odpowiednik w Claude Code. Agent ładuje je przy każdym zadaniu, więc każda linia kosztuje uwagę. Anthropic radzi poniżej 200 linii na plik. Badania z 2026 roku pokazują, że ogólne opisy repo nie podnoszą skuteczności, a podnoszą koszt. Wpisuj tylko to, czego agent nie wyczyta sam z repo.

## Standard AGENTS.md

- „A simple, open format for guiding coding agents”. Zwykły Markdown, bez wymaganych pól.
- Od 9 grudnia 2025 pod Agentic AI Foundation w Linux Foundation. Projekty założycielskie: MCP (Anthropic), goose (Block), AGENTS.md (OpenAI).
- Strona deklaruje użycie w „over 60k open-source projects”. Obsługują go m.in. Codex, Cursor, GitHub Copilot coding agent, Gemini CLI, Jules, Devin, Windsurf, Junie, Aider, goose, opencode, Zed, Warp, VS Code, Amp.
- Pliki zagnieżdżone: „The closest AGENTS.md to the edited file wins; explicit user chat prompts override everything.”

## Jak ładują to narzędzia

**Claude Code (CLAUDE.md):**
- Kolejność od ogólnego do szczegółowego: polityka firmy → `~/.claude/CLAUDE.md` → `./CLAUDE.md` albo `./.claude/CLAUDE.md` → `./CLAUDE.local.md` (poza gitem).
- Importy `@ścieżka`, do czterech poziomów. Pomagają uporządkować plik, ale „don't reduce its context cost”.
- `.claude/rules/*.md` z `paths:` ładują się tylko przy pasujących plikach.
- AGENTS.md: Claude Code czyta go, gdy nie ma CLAUDE.md. Gdy są oba, czyta tylko CLAUDE.md, chyba że CLAUDE.md importuje `@AGENTS.md` (od v2.1.277).
- „Claude treats them as context, not enforced configuration.” Zakaz, który musi działać zawsze, idzie do hooka `PreToolUse`.
- „if two instructions contradict each other, Claude may pick one arbitrarily”. Audyt: `/doctor prompt-audit`.

**Codex:**
- Globalny plik w `~/.codex`, potem każdy katalog od korzenia repo do bieżącego. W katalogu: `AGENTS.override.md`, potem `AGENTS.md`, potem nazwy zapasowe. „Codex includes at most one file per directory.”
- Pliki są sklejane. Bliższe katalogowi roboczemu są później i wygrywają.
- Limit `project_doc_max_bytes` = 32 KiB łącznie. Po przekroczeniu Codex przestaje dodawać pliki.

**Cursor:**
- Reguły w `.cursor/rules/*.mdc` z polami `description`, `globs`, `alwaysApply`. Cursor obsługuje też AGENTS.md w korzeniu i podkatalogach.
- „Keep rules under 500 lines”. „Start simple. Add rules only when you notice Agent making the same mistake repeatedly”.

## Długość — co mówią źródła

| Źródło | Próg |
|---|---|
| Anthropic (memory docs) | „target under 200 lines per CLAUDE.md file. Longer files consume more context and reduce adherence.” |
| HumanLayer | „general consensus” poniżej 300 linii, „shorter is even better”. Ich własny plik ma „less than sixty lines”. |
| Cursor | reguła poniżej 500 linii |
| Codex | 32 KiB łącznie (limit techniczny). „A short, accurate `AGENTS.md` is more useful than a long file full of vague rules.” |

Żaden z tych progów nie ma opublikowanego eksperymentu za sobą.

**Ile instrukcji model wykona naraz.** IFScale (2025): 500 instrukcji typu „użyj słowa X”, 20 modeli. Najlepsze modele osiągnęły tylko „68% accuracy” przy 500 instrukcjach. Modele faworyzują instrukcje z początku. To syntetyczne zadanie, nie kod. HumanLayer wyprowadza z tego: „Frontier thinking LLMs can follow ~ 150-200 instructions with reasonable consistency”, a system prompt Claude Code ma już „~50 individual instructions”.

## Czy te pliki w ogóle pomagają

- **Gloaguen i in. (ETH, 2026):** „providing context files does not generally improve task success rates”, a koszt inferencji rośnie „by over 20% on average”. Agenci wykonują instrukcje, ale ogólne opisy repo nie pomagają. Narzędzia wymienione w pliku agenci używają dużo częściej. Liczby z wersji v1 (znane tylko ze streszczenia): pliki od ludzi ok. +4%, pliki z LLM ok. −3%.
- **Lulla i in. (2026):** 124 PR w 10 repo. Z AGENTS.md mediana czasu niższa o 28,64%, tokenów wyjścia mniej o 16,58%, ukończenie „similar”. Mierzy wydajność, nie poprawność.
- **Khatri (2026):** Claude Code i Codex, 17 zadań, 288 uruchomień. Strategia kontekstu nie zmieniła poprawności w mierzalny sposób. Porażki brały się z umiejętności implementacji, nie z braku wiedzy o repo.
- **Vercel (2026):** skrócony indeks wiedzy w AGENTS.md (8KB) dał 100%, ten sam materiał jako skill 79%. Skill nie został wywołany w 56% przypadków.

> **Status: Disputed** — Gloaguen i Khatri: brak zysku w skuteczności. Lulla: zysk w czasie i tokenach. Vercel: AGENTS.md lepszy niż skill dla wiedzy potrzebnej zawsze. Badania mierzą różne rzeczy.

## Co wpisać, czego nie

Wpisz:
- komendy build, test, lint, których agent nie zgadnie,
- narzędzia specyficzne dla projektu (agent ich używa, gdy są w pliku),
- konwencje niestandardowe, odmienne od typowych dla języka,
- krótką mapę: co gdzie jest i dlaczego (HumanLayer: WHAT, WHY, HOW),
- reguły „zawsze rób X”.

Nie wpisuj:
- stylu kodu — HumanLayer: „Never send an LLM to do a linter's job.” Formatter w hooku,
- ogólnego opisu architektury, który agent wyczyta z kodu — Claude Code: „Only write down what Claude can't find by reading the repo”,
- procedur na wiele kroków — to skill albo reguła z `paths:` ([Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md)),
- fragmentów kodu — lepiej wskazówka `plik:linia`,
- zakazów, które muszą działać zawsze — to hook albo uprawnienia.

## Jak stosować

1. Nie generuj pliku na ślepo (`/init`). HumanLayer odradza, bo to „the highest leverage point of the harness”. Pliki z LLM wypadły słabiej u Gloaguen. Jeśli używasz `/init`, potnij wynik.
2. Zacznij od kilkunastu linii: komendy, nietypowe narzędzia, nietypowe konwencje.
3. Dopisuj reaktywnie. Claude Code: agent pomylił konwencję albo komendę dwa razy → dopisz. Codex: gdy błąd się powtarza, poproś agenta o retrospektywę i zaktualizuj plik.
4. Trzymaj plik poniżej 200 linii. Długie, rzadko potrzebne części przenieś do `.claude/rules/` z `paths:` albo do skilli.
5. Kilka narzędzi w zespole → AGENTS.md jako główny plik, CLAUDE.md z jedną linią `@AGENTS.md`.
6. Co jakiś czas szukaj sprzeczności i nieaktualnych reguł.
7. Ważne zakazy przenieś do hooków. Instrukcja to prośba, nie gwarancja.

## Zobacz też
- [Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md) — wiedza ładowana na żądanie
- [Context engineering dla agentów kodujących](context-engineering.md) — dlaczego każda linia kosztuje
- [Jak przygotować repo i agenta do pracy](agent-setup.md) — proces przygotowania repo dla agenta
- [DESIGN.md — design system w jednym pliku dla agenta](../design/design-md.md) — DESIGN.md: ten sam pomysł dla designu

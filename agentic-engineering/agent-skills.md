---
title: Agent Skills — jak pisać skille i kiedy ich używać
updated: 2026-10-28
tags: [skills, skill-md, progressive-disclosure, claude-code, codex, evals]
sources:
  - "[Equipping agents for the real world with Agent Skills (Anthropic)](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) — 2025-10-16 — high"
  - "[Skill authoring best practices (Anthropic)](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) — unknown — high"
  - "[Claude Code — Skills](https://code.claude.com/docs/en/skills) — unknown — high"
  - "[Claude Code — Extend Claude Code (features overview)](https://code.claude.com/docs/en/features-overview) — unknown — high"
  - "[agentskills.io](https://agentskills.io/) — unknown — high"
  - "[Codex — Build skills (OpenAI)](https://developers.openai.com/codex/skills) — unknown — high"
  - "[Testing Agent Skills Systematically with Evals (OpenAI)](https://developers.openai.com/blog/eval-skills) — unknown — high"
  - "[Claude Skills are awesome, maybe a bigger deal than MCP (Simon Willison)](https://simonwillison.net/2025/Oct/16/claude-skills/) — 2025-10-16 — high"
  - "[OpenAI are quietly adopting skills (Simon Willison)](https://simonwillison.net/2025/Dec/12/openai-skills/) — 2025-12-12 — high"
  - "[Superpowers (Jesse Vincent)](https://blog.fsck.com/2025/10/09/superpowers/) — 2025-10-09 — medium"
  - "[AGENTS.md outperforms skills in our agent evals (Vercel)](https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals) — 2026-01-28 — medium"
  - "[anthropics/skills — skill-creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator) — unknown — high"
---

# Agent Skills — jak pisać skille i kiedy ich używać

> Skill to folder z plikiem `SKILL.md` i opcjonalnymi skryptami i materiałami. Agent widzi na start tylko nazwę i opis. Resztę ładuje, gdy zadanie pasuje. Dzięki temu możesz mieć wiele skilli bez zapychania kontekstu. Najważniejszy jest opis, bo od niego zależy, czy skill się włączy. Skill trzeba testować: z nim i bez niego, na kilku scenariuszach.

## Co to jest

- Format od Anthropic (październik 2025), potem otwarty standard na agentskills.io. Skill = folder z `SKILL.md` i opcjonalnie `scripts/`, `references/`, `assets/`.
- Trzy poziomy ładowania (progressive disclosure): metadane (nazwa, opis) → treść `SKILL.md` → pliki powiązane. Dołączona wiedza jest „effectively unbounded” (Anthropic).
- Willison: ok. 50 tokenów na skill, dopóki się nie załaduje. Serwer GitHub MCP potrafi zająć „tens of thousands of tokens”. Nazwał skille „maybe a bigger deal than MCP”.
- Codex obsługuje skille: `.agents/skills` (w repo i wyżej), `$HOME/.agents/skills`, `/etc/codex/skills`. Lista skilli zajmuje „at most 2% of the model's context window, or 8,000 characters”.
- Claude Code: „Custom commands have been merged into skills”. Stare `.claude/commands/x.md` dalej działa.

## Limity i pola

- `name`: maks. 64 znaki, małe litery, cyfry, myślniki. Bez słów „anthropic” i „claude”.
- `description`: maks. 1 024 znaki, bez tagów XML. W Claude Code opis + `when_to_use` są ucinane na liście do 1 536 znaków.
- Treść `SKILL.md`: „Keep the SKILL.md body under 500 lines.”
- Pola Claude Code: `disable-model-invocation`, `user-invocable`, `context: fork`, `allowed-tools`, `paths`.
- Codex: `agents/openai.yaml` z `allow_implicit_invocation`.

## Jak pisać (Anthropic, OpenAI)

**Opis:**
- Mówi, co skill robi i kiedy go użyć. Claude wybiera „from potentially 100+ available Skills”.
- „Always write in third person.”
- Codex: „Front-load the key use case and trigger words.”

**Treść:**
- „Default assumption: Claude is already very smart.” Pisz tylko to, czego model nie wie.
- Swoboda dopasowana do kruchości zadania: luźne wskazówki, gdy wiele dróg jest dobrych; dokładny skrypt, gdy błąd jest kosztowny.
- Odnośniki tylko jeden poziom w głąb. Plik referencyjny powyżej 100 linii dostaje spis treści.
- Nazwy w formie odczasownikowej (`processing-pdfs`). Spójne nazewnictwo. Bez informacji, które się zestarzeją.
- Codex: „Keep each skill focused on one job.” „Prefer instructions over scripts unless you need deterministic behavior.”
- Skille z efektami ubocznymi (deploy, wysyłka): `disable-model-invocation: true`, żeby uruchamiał je tylko człowiek.

**Testy:**
- Anthropic: „Create evaluations BEFORE writing extensive documentation”. „At least three evaluations”. Test na Haiku, Sonnet i Opus. Pisz skill z jednym Claude (A), testuj na drugim (B). „There is not currently a built-in way to run these evaluations.”
- OpenAI: „a small set of 10–20 prompts is enough”. Co najmniej jeden przypadek `should_trigger=false`. Sprawdzenia deterministyczne na wyjściu `codex exec --json`.
- `skill-creator` w anthropics/skills ma tryby eval, benchmark i optymalizacji opisu.
- Jesse Vincent (Superpowers): pisanie skilli jak TDD. Testuj na subagentach w realistycznych „pressure scenarios”. Pierwsze testy nie działały, bo Claude „quizzing the subagents like they were on a gameshow”.

**Bezpieczeństwo:** „We recommend installing skills only from trusted sources.” Przejrzyj skrypty i wywołania sieci przed instalacją (Anthropic).

## Co wybrać: CLAUDE.md, rules, skill, subagent, MCP, hook

Według features overview Claude Code:

| Mechanizm | Do czego | Ładowanie |
|---|---|---|
| CLAUDE.md / AGENTS.md | reguły „zawsze rób X”, komendy | zawsze |
| `.claude/rules/` z `paths:` | wskazówki dla części repo | przy pasujących plikach |
| Skill | wiedza referencyjna i procedury | opis zawsze, treść na żądanie |
| Subagent | izolacja kontekstu | wraca tylko streszczenie |
| MCP | dostęp do zewnętrznych usług | definicje narzędzi |
| Hook | twarde wymuszenie | zawsze, deterministycznie |

Kiedy dodać:
- „Claude gets a convention or command wrong twice” → CLAUDE.md.
- Ten sam playbook wklejasz „for the third time” → skill.
- Zakaz musi działać zawsze → hook. „an instruction like 'never edit .env' … is a request, not a guarantee.”

## Spór: skill czy wiedza ładowana zawsze

- Vercel: skill nie włączył się w 56% przypadków. Ten sam materiał jako indeks w AGENTS.md dał 100% kontra 79%.
- Anthropic i OpenAI promują progressive disclosure, żeby oszczędzać kontekst.
- Odczyt komentatorów: wiedza potrzebna zawsze → AGENTS.md; procedura dla konkretnego typu zadania → skill.
- Skille pisane przez LLM: Anthropic poleca pisanie z Claude. Gloaguen pokazał, że pliki kontekstu z LLM lekko szkodzą ([AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md)).

## Jak stosować

1. Twórz skill, gdy trzeci raz wklejasz tę samą instrukcję.
2. Najpierw zrób 3+ scenariusze testowe i sprawdź, jak agent radzi sobie bez skilla.
3. Opis wg wzoru: „[Robi X, Y, Z]. Use when [sytuacje, słowa-klucze, typy plików].” Trzecia osoba. Słowa-klucze na początku.
4. Treść poniżej 500 linii. Szczegóły do `references/`, jeden poziom w głąb.
5. Tylko to, czego model nie wie: Twoje konwencje, kolejność kroków, pułapki, przykłady.
6. Testuj: z nim i bez niego, czy się włącza (i czy nie włącza się przy złych promptach), na modelach, których używasz.
7. Skill z efektem ubocznym: `disable-model-invocation: true`.
8. Wiedza potrzebna przy każdym zadaniu nie idzie do skilla, tylko do AGENTS.md.

## Zobacz też
- [AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md) — wiedza ładowana zawsze
- [Context engineering dla agentów kodujących](context-engineering.md) — progressive disclosure jako technika kontekstu
- [Katalog popularnych skilli do designu (skills.sh)](../design/design-skills-catalog.md) — przykłady popularnych skilli do designu
- [Wytyczne Anthropic do designu frontendu z Claude](../design/anthropic-frontend-design.md) — przykład skilla od Anthropic

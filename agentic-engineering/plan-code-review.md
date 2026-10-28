---
title: Plan → kod → review — jak zrobić zadanie z agentem kodującym
updated: 2026-10-28
tags: [process, workflow, planning, tdd, review, claude-code, codex]
sources:
  - "[Context engineering dla agentów kodujących](context-engineering.md)"
  - "[Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy](session-management.md)"
  - "[Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md)"
  - "[Spec-driven development (SDD)](spec-driven-development.md)"
  - "[Subagenty i praca wieloagentowa](subagents.md)"
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[Codex best practices (OpenAI)](https://learn.chatgpt.com/guides/best-practices) — unknown — high"
  - "[Advanced Context Engineering for Coding Agents (HumanLayer)](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md) — unknown — medium"
  - "[Everything We Got Wrong About Research-Plan-Implement (Dex Horthy) — przez streszczenie Dark Factory Dev](https://darkfactory.dev/news/2026-08-06-morning/story-3) — 2026-08-06 — medium"
  - "[Dex Horthy on RPI and Ralph (Dev Interrupted)](https://linearb.io/dev-interrupted/podcast/dex-horthy-humanlayer-rpi-methodology-ralph-loop) — 2026-02-17 — medium"
  - "[Agentic Engineering Patterns (Simon Willison)](https://simonwillison.net/guides/) — 2026 — high"
  - "[My LLM codegen workflow atm (Harper Reed)](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/) — 2025-02-16 — high"
  - "[My LLM coding workflow going into 2026 (Addy Osmani)](https://addyosmani.com/blog/ai-coding-workflow/) — 2025-12 — high"
  - "[Augmented Coding: Beyond the Vibes (Kent Beck)](https://newsletter.kentbeck.com/p/augmented-coding-beyond-the-vibes) — 2025-06-25 — high"
  - "[Agentic engineering (IBM Think)](https://www.ibm.com/think/topics/agentic-engineering) — 2026 — medium"
---

# Plan → kod → review — jak zrobić zadanie z agentem kodującym

> Wszystkie poważne źródła mają ten sam szkielet: najpierw zrozum i zaplanuj, potem koduj małymi krokami z testami, na końcu sprawdź w świeżym kontekście i przeczytaj kod sam. Plan powstaje w jednej sesji, kod w drugiej, review w trzeciej. Ciężar procesu dopasowujesz do zadania: mała poprawka to jeden prompt z testem, duża funkcja to spec i pełny cykl.

## Agentic engineering, nie vibe coding

- Karpathy ukuł „vibe coding” 3 lutego 2025. W lutym 2026 zaproponował „agentic engineering”: „'agentic' because the new default is that you are not writing the code directly 99% of the time, you are orchestrating agents who do and acting as oversight. 'engineering' to emphasize that there is an art & science and expertise to it.” Cytat znam ze źródeł wtórnych. Kto pierwszy użył terminu, jest sporne.
- Willison: „I use the term agentic engineering to describe the practice of developing software with the assistance of coding agents.” „Vibe coding” zostawia dla „unreviewed, prototype-quality LLM-generated code”.
- Różnica to review i odpowiedzialność za kod. Beck: „In augmented coding you care about the code, its complexity, the tests, & their coverage.”

## Warianty procesu ze źródeł

| Źródło | Kroki |
|---|---|
| Claude Code docs | wywiad → SPEC.md → nowa sesja buduje → weryfikacja (`/goal` albo testy) → niezależne review (`/code-review`) |
| Codex | prompt: cel, kontekst, ograniczenia, „done when” → `/plan` → kod w worktree → testy → `/review` → retrospektywa do AGENTS.md |
| HumanLayer RPI (2025) | research → plan → implement, kompakcja do plików, kontekst 40–60%, człowiek czyta research i plan |
| HumanLayer (2026, ze streszczenia) | krótki „structure outline” zamiast 8-stronicowego planu, mniejsze prompty po kolei, człowiek czyta też kod. RPI „falls flat for greenfield” |
| Harper Reed | wywiad „Ask me one question at a time…” → `spec.md` → `prompt_plan.md` i `todo.md` → wykonanie krok po kroku z testami |
| Willison | red/green TDD: „It's important to confirm that the tests fail before implementing the code.” |
| Beck | red-green-refactor, jeden test naraz, osobne commity dla zmian struktury i zachowania |

## Proces

### 0. Dobierz ciężar (decyzja Cortexu)
- **Mała poprawka, bug** → od razu krok 3 z testem odtwarzającym błąd.
- **Funkcja w znanym kodzie** → krótki plan (krok 2), bez pełnego speca.
- **Duża funkcja, wiele decyzji, kilka sesji** → spec (krok 1) albo narzędzie SDD ([Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl](sdd-tools.md)).

### 1. Zrozum i zapisz spec (sesja A)
- Poproś agenta o wywiad: „Ask me one question at a time so we can develop a thorough, step-by-step spec for this idea” (Harper Reed).
- Research kodu oddaj subagentowi, żeby nie zapchać kontekstu ([Subagenty i praca wieloagentowa](subagents.md)).
- Zapisz SPEC.md: cel, zachowanie, przypadki brzegowe, kryteria „gotowe”, jak sprawdzić.
- Przeczytaj i popraw spec. Pomyłka w researchu potrafi dać „thousands of bad lines of code” (HumanLayer).

### 2. Plan (sesja A albo B)
- Plan mode: `/plan` albo Shift+Tab (Claude Code, Codex).
- Plan krótki: które pliki, jaka struktura, kolejność kroków, jakie testy. HumanLayer 2026 skrócił plan do ok. 2 stron.
- Przeczytaj plan. Popraw kierunek teraz, nie w kodzie.

### 3. Kod (nowa sesja)
- Zacznij czystą sesję ze SPEC.md i planu ([Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy](session-management.md)).
- Najpierw test, który nie przechodzi. Potwierdź, że nie przechodzi. Potem kod.
- Przykład z Claude Code: „users report login fails after the session times out. look at token refresh in src/auth/, write a failing test that reproduces it, then fix it”.
- Małe kroki. Osmani: duże zlecenia dają „jumbled mess”.
- Dwie nieudane poprawki → `/clear` i lepszy prompt.
- Agent ma uruchomić testy i pokazać komendę z wynikiem.

### 4. Review (świeży kontekst)
- `/code-review`, Codex `/review` albo subagent tylko do odczytu, sprawdzający diff ze SPEC.md.
- Naprawiaj tylko błędy poprawności. Recenzent „will always find *something*”.
- Sprawdź, czy agent nie usunął ani nie osłabił testów.
- Szczegóły: [Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md).

### 5. Przeczytaj kod sam i zamknij
- Przeczytaj diff i opis PR. Willison: „Don't file pull requests with code you haven't reviewed yourself.”
- Nie commituj kodu, którego nie umiesz wyjaśnić (Osmani).
- Agent powtórzył ten sam błąd → dopisz regułę do AGENTS.md / CLAUDE.md ([AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md)).
- Trzeci raz ta sama procedura → zrób z niej skill ([Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md)).

## Kiedy przerwać i interweniować (Beck, Claude Code)

- Agent kręci się w kółko.
- Agent dodaje funkcje, o które nie prosiłeś.
- Agent usuwa albo wyłącza testy.
- Agent twierdzi „gotowe” bez dowodu.

## Gotowy prompt startowy (decyzja Cortexu, złożony ze źródeł wyżej)

```
Cel: <co ma działać>.
Kontekst: <pliki, moduły, link do SPEC.md>.
Ograniczenia: <czego nie ruszać, styl, zależności>.
Gotowe, gdy: <test/komenda i oczekiwany wynik>.
Najpierw zaproponuj krótki plan i poczekaj na akceptację.
Potem: test, który nie przechodzi → kod → uruchom testy i pokaż komendę z wynikiem.
Jeśli test wydaje się błędny, powiedz o tym zamiast go obchodzić.
```

## Zobacz też
- [Jak przygotować repo i agenta do pracy](agent-setup.md) — jak przygotować repo i agenta przed pracą
- [Spec-driven development (SDD)](spec-driven-development.md) — cięższa wersja kroków 1–2
- [Agenci równolegle — worktree, praca w tle, headless](parallel-agents.md) — kilka zadań naraz
- [Dowody na produktywność z agentami kodującymi](productivity-evidence.md) — co wiemy o zysku z tego procesu

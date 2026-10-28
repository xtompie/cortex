---
title: Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy
updated: 2026-10-28
tags: [sessions, compaction, clear, handoff, claude-code, codex]
sources:
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[Claude Code — Explore the context window](https://code.claude.com/docs/en/context-window) — unknown — high"
  - "[Effective harnesses for long-running agents (Anthropic, Justin Young)](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — 2025-11-26 — high"
  - "[Effective context engineering for AI agents (Anthropic)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — 2025-09-29 — high"
  - "[Advanced Context Engineering for Coding Agents (HumanLayer)](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md) — unknown — medium"
  - "[Codex best practices (OpenAI)](https://learn.chatgpt.com/guides/best-practices) — unknown — high"
  - "[Fission-AI/OpenSpec — README](https://github.com/Fission-AI/OpenSpec) — 2026-10-28 — high"
---

# Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy

> Jedna sesja to jedna spójna jednostka pracy. Nową sesję zaczynasz przy nowym zadaniu, po napisaniu speca i po dwóch nieudanych poprawkach. Kompakcja jest wygodna, ale gubi część instrukcji. Przy pracy na wiele sesji stan trzymasz w plikach: spec, plan, plik postępu, commity.

## Kiedy nowa sesja albo `/clear`

Claude Code:
- „`/clear` between unrelated tasks. It costs nothing.”
- „after two failed corrections run `/clear` and write a better prompt instead of a third.”
- Po wywiadzie zapisz SPEC.md, potem „start a fresh session to build from it, so the build begins with a clean context and a written definition of done.”

Codex:
- „Keep one chat per coherent unit of work”.
- „staying in the same chat is often better because it preserves the reasoning trail”.
- „Fork only when the work truly branches.”
- Jeden z typowych błędów według Codex: jeden czat na cały projekt zamiast jednego czatu na jeden spójny wynik.

OpenSpec: „Clear your context before starting implementation.”

Obie strony zgadzają się co do zasady „jedna spójna jednostka pracy”. Różnią się akcentem. Codex chroni ślad rozumowania. Claude Code chroni czysty kontekst.

## Kompakcja

- `/compact` z celem, np. „`/compact keep the API changes and the test commands`”. Uwaga z dokumentacji: „`/compact` is itself a big request”.
- Claude Code kompaktuje automatycznie. Próg ustawisz przez `/autocompact 500k`. `/rewind` ma opcję „Summarize from here”.
- Co przetrwa kompakcję w Claude Code:
  - główny CLAUDE.md, auto memory i plan z plan mode — wracają z dysku,
  - do 5 ostatnio zmienianych plików; plik powyżej 5 000 tokenów wraca tylko jako ścieżka,
  - treść skilli: do 5 000 tokenów na skill i 25 000 łącznie.
- Co ginie: reguły z `paths:` i zagnieżdżone CLAUDE.md zostają tylko w streszczeniu.
- Cache: ok. 1 godziny w subskrypcji, 5 minut w API. Bezczynna sesja powyżej ok. 200K tokenów jest kompaktowana przed wygaśnięciem cache.

Anthropic o pracy wielosesyjnej: „compaction isn't sufficient”. Kompakcja „doesn't always pass perfectly clear instructions to the next agent.”

## Przekazanie pracy między sesjami

Wzorzec Anthropic dla długich zadań (harness post):
1. Agent inicjalizujący tworzy `init.sh`, `claude-progress.txt`, listę funkcji w JSON i pierwszy commit.
2. Lista funkcji ma 200+ pozycji, każda z `"passes": false`. JSON, bo model rzadziej błędnie nadpisuje JSON niż Markdown.
3. Każda kolejna sesja bierze jedną funkcję, testuje ją, aktualizuje plik postępu i commituje.
4. Typowe błędy bez tego: agent próbuje zrobić całą aplikację naraz albo za wcześnie ogłasza sukces.

HumanLayer: „frequent intentional compaction”. Zamiast czekać na automat, zapisujesz research i plan do plików, a potem zaczynasz czystą sesję z tych plików. Kontekst w przedziale 40–60%.

Codex: PLANS.md dla długiej, wieloetapowej pracy.

Claude Code: `/rename` i `claude --resume <nazwa>` dla pracy na kilka dni.

## Jak stosować

1. Nowe zadanie → `/clear` albo nowa sesja.
2. Agent dwa razy źle poprawił → `/clear`. Napisz lepszy prompt z tym, czego się nauczyłeś.
3. Skończony spec albo plan → zapisz do pliku, implementację zacznij w nowej sesji.
4. Długa sesja przed nowym etapem → `/compact` z celem, co zachować.
5. Reguły, które muszą przetrwać kompakcję, trzymaj w głównym CLAUDE.md. Najważniejsze instrukcje skilla daj na górę SKILL.md.
6. Praca na wiele dni → plik postępu (co zrobione, co dalej, jak uruchomić testy) i commit po każdym kroku. Szablon prompta na koniec sesji (decyzja Cortexu): „Zapisz w `PROGRESS.md`: co jest zrobione i sprawdzone, co jest w toku, następny krok, komendy do testów. Bez historii rozmowy.”

## Zobacz też
- [Context engineering dla agentów kodujących](context-engineering.md) — dlaczego długi kontekst szkodzi
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — gdzie w procesie zaczynać nową sesję
- [Spec-driven development (SDD)](spec-driven-development.md) — spec jako plik przekazania

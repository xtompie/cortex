---
topic: agentic-engineering
description: praca z agentami kodującymi (Claude Code, Codex): context engineering, AGENTS.md i skille, styl komunikacji, spec-driven development, plan → kod → review
discovered: 2026-10-28
---

# Agentic engineering

## Procesy
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — jak zrobić zadanie z agentem: spec, plan, kod z testem w nowej sesji, review w świeżym kontekście, własne czytanie kodu (2026-10-28)
- [Jak przygotować repo i agenta do pracy](agent-setup.md) — jak przygotować repo: szybkie testy, krótki AGENTS.md, hooki, skille, output style (2026-10-28)

## Kontekst i sesje
- [Context engineering dla agentów kodujących](context-engineering.md) — context rot, cztery sposoby psucia kontekstu, techniki, spór o okna 1M (2026-10-28)
- [Sesje agenta — kiedy nowa, /clear, kompakcja, przekazanie pracy](session-management.md) — kiedy nowa sesja i `/clear`, co przetrwa kompakcję, pliki przekazania (2026-10-28)
- [Subagenty i praca wieloagentowa](subagents.md) — kiedy subagent, czego nie daje, koszt w tokenach, spór o wiele agentów (2026-10-28)
- [Agenci równolegle — worktree, praca w tle, headless](parallel-agents.md) — worktree, `/batch`, headless, lista kontrolna przed pracą bez nadzoru (2026-10-28)

## Instrukcje dla agenta
- [AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md) — AGENTS.md i CLAUDE.md: ładowanie w narzędziach, długość, badania o skuteczności, co wpisać (2026-10-28)
- [Agent Skills — jak pisać skille i kiedy ich używać](agent-skills.md) — jak pisać skille: opis, limity, testy, kiedy skill, a kiedy CLAUDE.md, hook, MCP (2026-10-28)
- [Styl komunikacji agenta — output styles, zwięzłość, uczciwe raporty](agent-communication-style.md) — output styles, zwięzłość, fałszywe raporty o sukcesie (2026-10-28)

## Jakość
- [Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md) — weryfikacja z dowodem, recenzent w świeżym kontekście, czytanie kodu przez człowieka (2026-10-28)
- [Dowody na produktywność z agentami kodującymi](productivity-evidence.md) — METR, DORA, akceptacja PR od agentów (2026-10-28)

## Spec-driven development
- [Spec-driven development (SDD)](spec-driven-development.md) — poziomy SDD, krytyka, badania, kiedy warto (2026-10-28)
- [Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl](sdd-tools.md) — Spec Kit, OpenSpec, Kiro, BMAD, Tessl i jak wybrać (2026-10-28)

---
title: Agenci równolegle — worktree, praca w tle, headless
updated: 2026-10-28
tags: [parallel-agents, worktree, headless, background-agents, claude-code, codex]
sources:
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[Codex best practices (OpenAI)](https://learn.chatgpt.com/guides/best-practices) — unknown — high"
  - "[Codex — Subagents (OpenAI)](https://learn.chatgpt.com/docs/agent-configuration/subagents) — unknown — high"
  - "[Agentic Coding Recommendations (Armin Ronacher)](https://lucumr.pocoo.org/2025/6/12/agentic-coding/) — 2025-06-12 — high"
  - "[Multi-Agents: What's Actually Working (Cognition)](https://cognition.com/blog/multi-agents-working) — 2026-04-22 — high"
---

# Agenci równolegle — worktree, praca w tle, headless

> Kilka agentów naraz działa, gdy każdy ma osobną kopię repo (git worktree) i osobne, rozłączne zadanie. Druga sesja to też najprostszy niezależny recenzent. Automatyzuj (headless, harmonogram) dopiero zadanie, które działa niezawodnie ręcznie.

## Narzędzia

Claude Code:
- `claude -w feature-auth` — sesja w osobnym worktree.
- `/batch` — „splits the work into 5 to 30 units… opens a PR for each”.
- `claude agents` — podgląd wielu agentów (research preview).
- `claude -p` — tryb bez interfejsu, do CI, hooków git i pętli. `--bare` daje powtarzalne uruchomienia.
- „A second session is also the easiest independent reviewer you can get.”

Codex:
- Zadania na żywo w git worktree.
- Automatyzacje: „skills define the method and scheduled tasks define the schedule”. Harmonogram dopiero wtedy, gdy zadanie działa ręcznie.
- Równolegle czytanie, ostrożnie z pisaniem: „Be more careful with parallel write-heavy workflows”.

## Zasady

- Ronacher: „parallelization boosts overall efficiency”. Narzędzia dla agenta muszą być szybkie: „Tools need to be fast”, „Crashes are tolerable; hangs are problematic”.
- Cognition (2026): zapisy w jednym wątku, pozostali agenci dokładają wiedzę, nie zmiany.

## Lista kontrolna przed pracą bez nadzoru (Claude Code)

- „Does it know what done looks like?”
- „Can it check its own work?”
- „What's it allowed to touch?”

## Jak stosować

1. Jedno zadanie = jeden worktree = jedna sesja.
2. Dziel pracę tak, żeby zadania nie dotykały tych samych plików.
3. Każde zadanie ma kryterium „gotowe” i sposób sprawdzenia (test, komenda).
4. Uprawnienia zawężone do tego, czego zadanie potrzebuje.
5. Wyniki każdego agenta przechodzą zwykłe review ([Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md)).

## Zobacz też
- [Subagenty i praca wieloagentowa](subagents.md) — równoległość wewnątrz jednej sesji
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — proces dla pojedynczego zadania

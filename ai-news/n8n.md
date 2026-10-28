---
title: n8n — automatyzacja workflow z AI
updated: 2026-10-28
tags: [n8n, automation, workflow, mcp, agents]
sources:
  - "[n8n-io/n8n — GitHub](https://github.com/n8n-io/n8n) — 2026-10-28 — high"
  - "[Introducing n8n 3.0 (blog n8n)](https://blog.n8n.io/introducing-n8n-v3/) — 2026-10-27 — high"
  - "[Release n8n@3.0.0 — GitHub](https://github.com/n8n-io/n8n/releases/tag/n8n%403.0.0) — 2026-10-27 — high"
  - "[n8n Community — Announcing n8n version 3.0](https://community.n8n.io/t/announcing-n8n-version-3-0-coming-soon/324016) — 2026 — high"
  - "[then8nblog — n8n v3 update: two changes missing from the 3.0 docs](https://then8nblog.com/news/n8n-3-0-undocumented-changes) — 2026-10 — low"
---

# n8n — automatyzacja workflow z AI

> n8n to platforma do automatyzacji: workflow składasz wizualnie, a tam, gdzie trzeba, dopisujesz kod. Ma ponad 400 integracji, węzły AI Agent oraz obsługę MCP jako klient i jako serwer. Licencja to fair-code, nie open source. ★209k. 27 października 2026 wyszła beta n8n 3.0. Stabilna wersja ma wyjść w grudniu. Wersja 3.0 to porządki i bezpieczeństwo, a nie nowe funkcje.

## Stan na 2026-10-28

- Linie wydań: `n8n@3.0.1` (beta, tylko obrazy Docker), `n8n@2.45.5` (stabilna) i `n8n@1.123.89` (stara).
- Wsparcie: 2.x dostaje poprawki bezpieczeństwa przez 12 miesięcy od stabilnej 3.0. Wsparcie 1.x kończy się 31 grudnia 2026.

## Ostatnie zmiany: n8n 3.0 (beta od 2026-10-27)

- **Self-hosting tylko przez Docker.** `npm` i `npx n8n` przestają być wspierane. Kubernetes i Helm działają bez zmian.
- **Queue mode:** ręczne uruchomienia zawsze idą na workery.
- **Dane binarne:** usunięty tryb in-memory. Zostają system plików albo S3 czy inny zewnętrzny storage.
- **Usunięte stare węzły:** Function, Function Item, Item Lists, Cron, Interval, Read/Write Binary File, Read PDF, HTML Extract, iCalendar, stare węzły OpenAI i część starych węzłów AI. Znika też AI Agent v1.
- **Ostrzejsze domyślne ustawienia:** Code node ma timeout 60 s zamiast 300 s. Niezweryfikowane pakiety społeczności są wyłączone, więc już zainstalowane przestają się ładować. Lista blokad SSRF jest dłuższa. Rotacja klucza szyfrowania jest zawsze włączona. Dane logowania Slacka wymagają signing secret.
- **Wyłączone:** Chat Hub jest domyślnie wyłączony (w 3.x da się go włączyć). Znika import z URL w edytorze.
- **Drobne nowości:** agent w Slacku może odpowiadać tylko na wzmianki. Serwery n8n Connect są w rejestrze MCP. Doszły endpointy API do zależności workflow, danych logowania i tabel danych.
- **Migration Report:** narzędzie, które samo naprawia wiele problemów. Opublikowane workflow działają dalej na v2 w czasie migracji.
- Blog spoza n8n podaje też zmiany, których nie ma w dokumentacji. CSP edytora przechodzi z trybu report-only na wymuszony, a znika `N8N_WORKFLOW_TAGS_DISABLED`. To źródło niskiej wiarygodności.

## Jak stosować

- Masz n8n na `npm`? Zaplanuj przejście na Dockera przed grudniem.
- Przed aktualizacją uruchom Migration Report i poszukaj w workflow usuniętych węzłów (Function, Cron, stare OpenAI).
- Workflow z długim kodem w Code node: sprawdź, czy mieszczą się w 60 s.
- n8n jako serwer MCP pozwala wywoływać Twoje workflow z Claude Code jak zwykłe narzędzia.

## Zobacz też
- [Model Context Protocol (MCP) — stan 2026](mcp.md) — protokół, przez który n8n łączy się z agentami

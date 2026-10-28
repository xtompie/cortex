---
topic: design
description: projektowanie stron i interfejsów, SVG, grafika na web, design z pomocą LLM
discovered: 2026-10-28
---

# Design

## Procesy
- [Proces projektowania strony z LLM — od pytań do krytyki](design-process.md) — jak zaprojektować stronę z LLM: pytania, idea z tematu i 3 kierunki, plan tokenów, przegląd, budowa, przegląd na zrzutach (2026-10-28)
- [Workflow generowania SVG przez LLM](svg-workflow-llm.md) — jak LLM ma robić SVG: plan sceny, prymitywy, render i poprawki, krzywe Béziera na końcu (2026-10-28)
- [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) — jak przejrzeć design: reguły Vercel w kodzie, heurystyki Nielsena i P0–P3, 14 przejść po zrzutach z punktacją (2026-10-28)

## Podstawy
- [Podstawy web designu dla developera](web-design-fundamentals.md) — hierarchia, skala odstępów 8/4px, płynna typografia (Utopia, `clamp()`), layout, liczby z nagradzanych stron (2026-10-28)
- [Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md) — ruch w UI: kiedy animować, easing, czasy poniżej 300 ms, przegląd animacji (2026-10-28)
- [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md) — WCAG 2 jako wymóg, APCA jako dodatkowa kontrola, palety w OKLCH (2026-10-28)

## Design systemy
- [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md) — trzy warstwy tokenów, standard DTCG, `@theme` w Tailwind v4, tokeny w shadcn/ui (2026-10-28)
- [DESIGN.md — design system w jednym pliku dla agenta](design-md.md) — DESIGN.md od Google: design system w jednym pliku dla agenta (2026-10-28)

## Design z LLM
- [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md) — wytyczne Anthropic: skill `frontend-design`, proces od tokenów do krytyki zrzutów, Claude Design (2026-10-28)
- [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md) — kierunek z tematu: tryby strony, inwentarz tematu, zdanie idei, test konkurenta, strategia koloru (2026-10-28)
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — typowe wyglądy designu z AI, lista odmowy i checklista (2026-10-28)
- [Prompty do sterowania estetyką designu](design-prompting.md) — jak sterować estetyką w prompcie, szablon briefu (2026-10-28)
- [Katalog popularnych skilli do designu (skills.sh)](design-skills-catalog.md) — popularne skille do designu ze skills.sh: co robią, jak instalować, popularność (2026-10-28)
- [Narzędzia AI do designu i design-to-code (2026)](ai-design-tools-2026.md) — Figma MCP, Google Stitch, Claude Design, v0, Lovable, Bolt i jak wybrać (2026-10-28)

## SVG
- [Techniki SVG na web — viewBox, prymitywy, dostępność, animacja](svg-techniques.md) — viewBox, prymitywy kontra ścieżki, `currentColor`, ikony, dostępność, animacja (2026-10-28)
- [Narzędzia SVG — render, optymalizacja, modele i benchmarki](svg-tools.md) — render (resvg, rsvg-convert), SVGO v4, modele StarVector i OmniSVG, benchmarki (2026-10-28)

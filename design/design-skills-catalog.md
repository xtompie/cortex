---
title: Katalog popularnych skilli do designu (skills.sh)
updated: 2026-10-28
tags: [skills, agent-skills, frontend, design, review, motion, tools]
sources:
  - "[skills.sh — leaderboard](https://skills.sh) — 2026-10-28 — medium"
  - "[skills.sh — topic Design & UI](https://skills.sh/topic/design) — 2026-10-28 — medium"
  - "[skills.sh — docs](https://skills.sh/docs) — unknown — high"
  - "[vercel-labs/skills — README (CLI)](https://github.com/vercel-labs/skills) — unknown — high"
  - "[vercel-labs/agent-skills — web-design-guidelines](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines) — unknown — high"
  - "[pbakaus/impeccable — SKILL.md v4.8.0](https://github.com/pbakaus/impeccable) — unknown — high"
  - "[leonxlnx/taste-skill — tasteskill v2](https://github.com/leonxlnx/taste-skill) — unknown — medium"
  - "[nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) — unknown — medium"
  - "[emilkowalski/skills](https://github.com/emilkowalski/skills) — unknown — high"
  - "[arvindrk/extract-design-system](https://github.com/arvindrk/extract-design-system) — unknown — medium"
  - "[designed-by-ai/skills — design-mobile-apps](https://github.com/designed-by-ai/skills) — unknown — low"
---

# Katalog popularnych skilli do designu (skills.sh)

> skills.sh to katalog skilli dla agentów, prowadzony przez Vercel. Ranking liczy instalacje z anonimowej telemetrii CLI `skills`. W designie wyróżnia się pięć rodzin: Anthropic `frontend-design` (opisany w [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md)), Vercel `web-design-guidelines` (audyt kodu UI), `impeccable` (pełny proces z komendami i krytyką), `taste-skill` (kierunek artystyczny z badania 247 stron) i skille Emila Kowalskiego (ruch i detale). Wiedzę z nich rozpisują strony [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md), [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) i [Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md).

## Jak instalować

- Cała kolekcja: `npx skills add vercel-labs/agent-skills`.
- Jeden skill z kolekcji dla Claude Code: `npx skills add vercel-labs/agent-skills --skill web-design-guidelines -a claude-code`.
- Domyślnie instalacja trafia do projektu. Flaga `-g` instaluje skill dla wszystkich projektów.
- skills.sh prowadzi rutynowe audyty bezpieczeństwa, ale Vercel nie gwarantuje jakości ani bezpieczeństwa każdego skilla. Przeczytaj SKILL.md przed instalacją.

## Skille (stan 2026-10-28)

| Skill | Repo | Instalacje (skills.sh) | Gwiazdki repo | Do czego |
|---|---|---|---|---|
| `frontend-design` | anthropics/skills | 1.0M | — | estetyka frontendu, unikanie „AI slop” → [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md) |
| `web-design-guidelines` | vercel-labs/agent-skills | 796.8K | ~33k | audyt kodu UI według Web Interface Guidelines, wynik w formacie `plik:linia` |
| `design-taste-frontend` (tasteskill v2) | leonxlnx/taste-skill | 694.4K | ~104k | kierunek artystyczny stron: losowanie kierunku, idea z tematu, inspektor w przeglądarce, pętla zrzutów |
| `high-end-visual-design`, `minimalist-ui`, `industrial-brutalist-ui`, `redesign-existing-projects`, `brandkit`, `image-to-code` | leonxlnx/taste-skill | 390–460K każdy | ~104k | warianty stylu i zadań z tej samej rodziny |
| `ui-ux-pro-max` | nextlevelbuilder/ui-ux-pro-max-skill | 421.1K | ~142k | przeszukiwalna baza: 79 stylów, 192 palety, 74 pary fontów, 119 zasad UX, generator design systemu |
| `impeccable` (+ `critique`, `polish`, `bolder`, `quieter`, `distill`, `delight`) | pbakaus/impeccable | 368.4K | ~92k | pełny proces: PRODUCT.md, nowy kierunek, krytyka z punktacją, komendy dopracowania |
| `emil-design-eng`, `review-animations`, `apple-design`, `animation-vocabulary` | emilkowalski/skills | 245–396K | ~51k | filozofia detalu i ruchu, przegląd animacji |
| `shadcn` | shadcn/ui | 271.1K | — | komponenty shadcn/ui |
| `extract-design-system` | arvindrk/extract-design-system | — | ~260 | wyciąga tokeny (kolory, fonty, odstępy) z publicznej strony do `tokens.json` i `tokens.css` |
| `design-mobile-apps` | designed-by-ai/skills | 1.1M | ~20 | ekrany mobilne przez API płatnego serwisu Sleek (wymaga `SLEEK_API_KEY`) |

Liczba instalacji nie mierzy jakości. `design-mobile-apps` ma 1.1M instalacji przy około 20 gwiazdkach repo. To tylko klient API serwisu Sleek. Wysoką liczbę instalacji mogą mieć skille instalowane hurtowo albo podbijane.

## Czym się różnią

- **Generowanie kierunku:** `frontend-design` daje zasady i postawę. `taste-skill` i `impeccable` mają skrypty, które losują kierunek (`draw.mjs`, `concept-seed`), bo model sam zawsze wybiera domyślny wygląd kategorii. `ui-ux-pro-max` dobiera styl z bazy według typu produktu.
- **Przegląd:** `web-design-guidelines` sprawdza kod według reguł technicznych. `impeccable critique` ocenia UX heurystykami Nielsena. `taste-skill` ocenia zrzuty ekranu. `review-animations` ocenia sam ruch. Szczegóły → [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md).
- **Pytania do człowieka:** `impeccable` zadaje 2–3 pytania przed pracą. `taste-skill` przy niejasnym briefie każe zdecydować i napisać swoje odczytanie w jednej linii. Zobacz [Proces projektowania strony z LLM — od pytań do krytyki](design-process.md).
- **Zależności:** `taste-skill` wymaga Node 22+ i Chrome. `impeccable` ma własny plik binarny i hooki. `ui-ux-pro-max` potrzebuje Pythona. `web-design-guidelines` przy każdym przeglądzie pobiera świeże reguły z GitHuba.

## Jak stosować

- Audyt istniejącego UI: zainstaluj `web-design-guidelines` i każ przejrzeć konkretne pliki.
- Nowa strona marketingowa: `taste-skill` albo `impeccable`. Weź jeden, nie oba, bo ich procesy się wykluczają.
- Aplikacja albo dashboard: `impeccable` (tryb Operate) albo `taste-skill --app`.
- Ruch i interakcje: `emil-design-eng` przy budowie, `review-animations` przy przeglądzie.
- Bez instalowania: zasady z tych skilli są rozpisane w [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md), [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) i [Ruch w interfejsie — kiedy animować, easing, czasy, przegląd](motion-design.md). Proces z [Proces projektowania strony z LLM — od pytań do krytyki](design-process.md) działa bez żadnego skilla.

## Zobacz też
- [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md) — skill Anthropic i jego historia
- [Proces projektowania strony z LLM — od pytań do krytyki](design-process.md) — proces, który łączy te źródła
- [Narzędzia AI do designu i design-to-code (2026)](ai-design-tools-2026.md) — narzędzia poza skillami (Figma MCP, Stitch, Claude Design)

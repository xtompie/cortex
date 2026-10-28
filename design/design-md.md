---
title: DESIGN.md — design system w jednym pliku dla agenta
updated: 2026-10-28
tags: [design-md, design-system, agents, stitch, tokens]
sources:
  - "[google-labs-code/design.md](https://github.com/google-labs-code/design.md) — 2026-04-21 — high"
  - "[VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — 2026 — medium"
  - "[DESIGN.md: A Markdown Design System File for AI Coding Agents (Better Stack)](https://betterstack.com/community/guides/ai/design-md-ai/) — 2026 — medium"
  - "[What The Hell Is Google Stitch's DESIGN.md (DesignWhine)](https://www.designwhine.com/what-the-hell-is-google-stitchs-design-md/) — 2026 — low"
  - "[Design UI using AI with Stitch from Google Labs](https://blog.google/innovation-and-ai/models-and-research/google-labs/stitch-ai-ui-design/) — 2026-03-18 — high"
---

# DESIGN.md — design system w jednym pliku dla agenta

> DESIGN.md to otwarty format od Google Labs: tokeny w YAML (dokładne wartości) plus proza w Markdown (dlaczego i jak ich używać).
> Kładziesz go w root projektu obok `AGENTS.md`/`CLAUDE.md`. Agent generuje UI zgodne z Twoim stylem zamiast „domyślnego wyglądu AI”.
> Ma CLI do lintu (m.in. kontrast WCAG) i diffu wersji.

## Skąd się wziął

- Dodany do Google Stitch przy przebudowie w marcu 2026 jako sposób eksportu i importu systemu designu między projektami i narzędziami.
- 21 kwietnia 2026 Google Labs otworzyło specyfikację i CLI na licencji Apache 2.0: `google-labs-code/design.md` (~28.6k gwiazdek, październik 2026). Wersja schematu: `"alpha"`.
- `VoltAgent/awesome-design-md` (~124k gwiazdek) — kolekcja gotowych plików DESIGN.md opisujących style znanych marek. Wrzucasz plik do projektu i agent generuje pasujące UI.

## Format

Dwie warstwy:
1. **Tokeny YAML** — w front matter (`---`) albo w blokach ```` ```yaml ```` w sekcjach. To wartości normatywne.
2. **Proza Markdown** — sekcje `##` z uzasadnieniem: nastrój marki, kiedy użyć akcentu, czego unikać.

Schemat tokenów:

```yaml
version: alpha          # opcjonalnie
name: Heritage
colors:     { primary: "#1A1C1E", tertiary: "#B8422E", neutral: "#F7F5F2" }
typography: { h1: { fontFamily: Public Sans, fontSize: 3rem } }
rounded:    { sm: 4px, md: 8px }
spacing:    { sm: 8px, md: 16px }
components:
  button-primary:
    backgroundColor: "{colors.tertiary}"
    textColor: "{colors.on-tertiary}"
    rounded: "{rounded.sm}"
    padding: 12px
```

- Kolor: dowolny kolor CSS, także `oklch()`. Wymiar: `px`, `em`, `rem`. Referencje: `{colors.primary}`.
- Właściwości komponentów: `backgroundColor`, `textColor`, `typography`, `rounded`, `padding`, `size`, `height`, `width`. Warianty (hover, active) to osobne wpisy, np. `button-primary-hover`.

Kolejność sekcji (można pominąć, nie można przestawić):
1. Overview (alias: Brand & Style)
2. Colors
3. Typography
4. Layout (alias: Layout & Spacing)
5. Elevation & Depth
6. Shapes
7. Components
8. Do's and Don'ts

Zduplikowana sekcja albo zduplikowany klucz YAML = błąd. Nieznane sekcje i tokeny są akceptowane.

## CLI

```bash
npx @google/design.md lint DESIGN.md              # struktura, złe referencje, kontrast WCAG
npx @google/design.md diff DESIGN.md DESIGN-v2.md # regresje tokenów i prozy
```

Wynik to JSON, który agent może sam przetworzyć. Na Windows używaj aliasu `designmd`.

## Relacja do innych formatów

- **DTCG (`.tokens.json`)** — format wymiany tokenów między narzędziami. Brak prozy i uzasadnień. → [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md)
- **DESIGN.md** — tokeny + kontekst dla agenta LLM. Mniej typów, ale agent rozumie *dlaczego*.
- **AGENTS.md / CLAUDE.md** — jak pracować w repo. DESIGN.md mówi, jak ma wyglądać UI. W `CLAUDE.md` wystarczy `@DESIGN.md`.

## Jak stosować

- [ ] Utwórz `DESIGN.md` w root projektu. Zacznij od gotowego pliku z `awesome-design-md` albo wyeksportuj z Stitch (Stitch umie też wyciągnąć system z dowolnego URL).
- [ ] Tokeny trzymaj zgodne z tokenami w kodzie (Tailwind `@theme`, shadcn `:root`) — jedno źródło prawdy, drugie generowane albo sprawdzane.
- [ ] W sekcji Overview opisz nastrój jednym-dwoma zdaniami. Agent tego używa do decyzji, których tokeny nie pokrywają.
- [ ] Sekcja Do's and Don'ts: konkretne zakazy (np. „nie używaj gradientów”, „akcent tylko dla akcji”).
- [ ] Podepnij w `AGENTS.md`/`CLAUDE.md` (`@DESIGN.md`).
- [ ] Dodaj `designmd lint DESIGN.md` do CI albo pre-commita.

## Zobacz też

- [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md) — standard DTCG, Tailwind v4, shadcn/ui
- [Narzędzia AI do designu i design-to-code (2026)](ai-design-tools-2026.md) — Stitch, Figma MCP, Claude Design
- [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md) — progi kontrastu sprawdzane przez lint

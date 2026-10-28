---
title: Design tokens — DTCG, Tailwind v4, shadcn/ui
updated: 2026-10-28
tags: [design-tokens, design-system, tailwind, shadcn, dtcg]
sources:
  - "[Design Tokens Format Module (DTCG)](https://www.designtokens.org/tr/drafts/format/) — 2025.10 — high"
  - "[W3C Design Tokens Community Group](https://w3.org/community/design-tokens) — 2025-10-28 — high"
  - "[Design Tokens: the W3C DTCG standard explained (Beryl)](https://www.beryldesign.fr/en/post/design-tokens-w3c-dtcg) — 2025 — medium"
  - "[Design Tokens in 2026: The W3C Format, Explained (CODERCOPS)](https://blog.codercops.com/blog/design-tokens-2026-w3c-format-guide) — 2026 — low"
  - "[Tailwind CSS — Theme variables](https://tailwindcss.com/docs/theme) — unknown — high"
  - "[Tailwind CSS v4 Dynamic Themes (SitePoint)](https://www.sitepoint.com/tailwind-css-v4-dynamic-themes/) — 2026 — medium"
  - "[Design Tokens with Tailwind: A Theme That Survives a Rebrand](https://www.matthewswong.com/en/blog/design-tokens-tailwind-theme/) — 2026 — low"
  - "[shadcn/ui — Theming](https://ui.shadcn.com/docs/theming) — unknown — high"
  - "[shadcn/ui — Registry examples](https://ui.shadcn.com/docs/registry/examples) — unknown — high"
  - "[style-dictionary/style-dictionary](https://github.com/style-dictionary/style-dictionary) — 2026 — high"
---

# Design tokens — DTCG, Tailwind v4, shadcn/ui

> Design token to nazwana decyzja projektowa (kolor, odstęp, font, promień) zamiast wartości wpisanej na sztywno.
> Od października 2025 jest wspólny format wymiany: Design Tokens Format Module 2025.10 (W3C Community Group).
> W kodzie webowym tokeny żyją jako zmienne CSS: w Tailwind v4 w bloku `@theme`, w shadcn/ui jako semantyczne pary `background`/`foreground`.

## Trzy warstwy tokenów

1. **Prymitywy** — surowa paleta i skale: `--color-orange-500: oklch(0.71 0.19 41)`, `--spacing: 4px`.
2. **Semantyczne aliasy** — znaczenie, nie wartość: `--color-brand: var(--color-orange-500)`, `--color-danger`, `--color-muted`.
3. **Tokeny komponentów** — opcjonalne: `--color-button-primary-bg: var(--color-brand)`.

Komponenty używają tylko warstwy 2 i 3. Rebranding albo dark mode zmienia jedną wartość w warstwie 1 lub mapowanie w warstwie 2, a reszta podąża sama.

## Standard DTCG (Design Tokens Format Module)

- Pierwsza stabilna wersja **2025.10**, ogłoszona 28 października 2025. Po ok. pięciu latach prac i trzech draftach.
- To **Community Group Report**, nie formalna W3C Recommendation.
- Wsparcie zgłosiły m.in. Adobe, Google, Meta, Microsoft, Amazon i Figma. Narzędzia: Penpot, Sketch, Framer, zeroheight i inne.
- Pliki: `.tokens` lub `.tokens.json`. Media type: `application/design-tokens+json`.
- Zarezerwowane klucze: `$value`, `$type`, `$description`, `$extensions`, `$deprecated`, `$root`, `$extends`, `$ref`.
- `$type`: `color`, `dimension`, `fontFamily`, `fontWeight`, `duration`, `cubicBezier`, `number`, `strokeStyle`, `border`, `transition`, `shadow`, `gradient`, `typography`. `$type` może być dziedziczony z grupy.
- Aliasy: `{group.token}` albo JSON Pointer `"$ref": "#/group/token"`.
- Motywy i wiele marek: `$extends` i dziedziczenie grup, bez kopiowania plików.

```json
{
  "color": {
    "$type": "color",
    "orange-500": { "$value": "oklch(0.71 0.19 41)" },
    "brand": { "$value": "{color.orange-500}", "$description": "Główny kolor marki" }
  }
}
```

Konwersja DTCG → CSS / iOS / Android: Style Dictionary (`style-dictionary/style-dictionary`, ~4.9k gwiazdek).

## Tailwind v4 — `@theme`

Konfiguracja przeszła z `tailwind.config.js` do CSS. Zmienna w `@theme` to token **i** generator klas.

```css
@import "tailwindcss";

@theme {
  --color-mint-500: oklch(0.72 0.11 178);  /* bg-mint-500, text-mint-500, ... */
  --font-display: "Satoshi", sans-serif;   /* font-display */
  --breakpoint-3xl: 120rem;                /* 3xl: */
}
```

- Przestrzenie nazw → klasy: `--color-*`, `--font-*`, `--text-*` (rozmiar), `--font-weight-*`, `--leading-*`, `--tracking-*`, `--spacing-*`, `--radius-*`, `--shadow-*`, `--breakpoint-*`, `--container-*` (warianty `@sm:`), `--ease-*`, `--animate-*` i inne.
- Reset domyślnych wartości: `--color-*: initial;` (jedna przestrzeń) albo `--*: initial;` (wszystko — zostają tylko Twoje tokeny).
- `@theme inline` — gdy token wskazuje na inną zmienną. Bez `inline` łańcuch `var()` może się rozwiązać na złym elemencie DOM.
- `@theme` musi być na najwyższym poziomie. Zmienne, które nie mają generować klas, trzymaj w `:root`.
- Tokeny są żywymi zmiennymi CSS — można je nadpisać w selektorze (`[data-theme="dark"]`) bez przebudowy.

Wzorzec motywów w runtime:

```css
:root            { --primary: oklch(0.62 0.19 256); }
[data-theme=dark]{ --primary: oklch(0.72 0.19 256); }

@theme inline {
  --color-primary: var(--primary);
}
```

## shadcn/ui — semantyczne tokeny

- Komponenty używają semantycznych tokenów: `background`, `foreground`, `primary`, `muted`, `accent`, `destructive`, `border`, `ring`… Każdy kolor tła ma parę `*-foreground` na tekst.
- Wartości w OKLCH w `:root` i `.dark`, np. `--primary: oklch(0.205 0 0)`. Starsze wersje używały HSL bez funkcji koloru.
- `components.json`: `tailwind.cssVariables: true` (domyślnie) włącza tokeny jako zmienne CSS.
- Własny kolor: dodaj do `:root` i `.dark`, potem zmapuj w `@theme inline`.
- **Registry** w 2026 rozprowadza nie tylko komponenty, ale też style (`registry:style`) i motywy (`registry:theme`) z obiektem `cssVars` (`theme`, `light`, `dark`), a nawet instrukcje dla agentów.
- `shadcn/create` — podgląd kolorów, promienia, fontów i ikon, generuje preset.

## Jak stosować

- [ ] Nie wpisuj kolorów, odstępów ani fontów na sztywno w komponentach — tylko tokeny.
- [ ] Prymitywy w OKLCH (skala 50–950), semantyka jako aliasy, komponenty korzystają z semantyki.
- [ ] Każdy token tła ma parę `-foreground` sprawdzoną pod kontrast — [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md).
- [ ] Tailwind v4: tokeny w `@theme`, aliasy do zmiennych w `@theme inline`, reset `--color-*: initial` gdy chcesz wyłącznie własną paletę.
- [ ] Dark mode: nadpisuj zmienne w `.dark` / `[data-theme=dark]`, nie twórz osobnych klas.
- [ ] Wymiana z narzędziami (Figma, Penpot): eksport/import w formacie DTCG, generacja CSS przez Style Dictionary.
- [ ] Dla agenta AI: opisz tokeny i ich znaczenie w pliku [DESIGN.md — design system w jednym pliku dla agenta](design-md.md) albo w regułach projektu.

## Zobacz też

- [DESIGN.md — design system w jednym pliku dla agenta](design-md.md) — tokeny + uzasadnienie w jednym pliku dla agentów
- [Podstawy web designu dla developera](web-design-fundamentals.md) — skąd biorą się skale odstępów i fontów
- [Narzędzia AI do designu i design-to-code (2026)](ai-design-tools-2026.md) — Figma MCP czyta zmienne/tokeny z pliku Figmy

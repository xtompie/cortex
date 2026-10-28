---
title: Kolor i kontrast — OKLCH, WCAG 2, APCA
updated: 2026-10-28
tags: [color, contrast, accessibility, wcag, apca, oklch, dark-mode]
sources:
  - "[WebAIM Million 2026](https://webaim.org/projects/million/) — 2026 — high"
  - "[APCA Contrast vs WCAG 2: The Complete Guide (CSS DNA)](https://cssdna.com/blog/wcag-vs-apca-contrast/) — 2026-07-20 — medium"
  - "[WCAG 3.0 in September 2026 (Accessible Resources)](https://www.accessibleresources.com/post/wcag-3-september-2026-working-draft-explained) — 2026-09 — medium"
  - "[WCAG 2.2 vs WCAG 3.0 (Qualibooth)](https://www.qualibooth.com/resources/wcag-22-vs-30-whats-coming/) — 2026 — medium"
  - "[WCAG 3 readiness (Lavawall)](https://lavawall.com/wcag-3-readiness/) — 2026 — low"
  - "[Tailwind CSS v4 Dynamic Themes (SitePoint)](https://www.sitepoint.com/tailwind-css-v4-dynamic-themes/) — 2026 — medium"
  - "[Design Tokens That Scale in 2026 (Mavik Labs)](https://www.maviklabs.com/blog/design-tokens-tailwind-v4-2026/) — 2026 — low"
  - "[Refactoring UI](https://refactoringui.com/) — 2018 — high"
---

# Kolor i kontrast — OKLCH, WCAG 2, APCA

> Prawnie obowiązuje WCAG 2: 4.5:1 dla zwykłego tekstu, 3:1 dla dużego tekstu i elementów UI.
> APCA lepiej przewiduje czytelność (zwłaszcza w dark mode), ale nie jest oficjalną częścią WCAG 3 — używaj jej jako dodatkowej kontroli.
> Palety buduj w OKLCH: jasność jest w niej percepcyjnie równa, więc skale i warianty dark mode wychodzą przewidywalnie.

## Dlaczego to ważne

WebAIM Million 2026 (dane z lutego 2026): **83.9%** stron głównych z miliona najpopularniejszych miało tekst o za niskim kontraście, średnio **34** takie miejsca na stronę. To najczęstszy błąd dostępności w sieci.

## WCAG 2 — co obowiązuje dziś

- **AA:** 4.5:1 dla zwykłego tekstu. 3:1 dla dużego tekstu (24px+ albo 18.66px+ pogrubiony). 3:1 dla komponentów UI i grafik.
- **AAA:** 7:1 dla zwykłego tekstu, 4.5:1 dla dużego.
- Prawo wskazuje starsze wersje: WCAG 2.1 AA dla ADA Title II i dla EN 301 549 (European Accessibility Act), WCAG 2.0 A/AA dla Section 508.

Słabości wzoru WCAG 2:
- Zamiana tekstu z tłem daje ten sam wynik, choć percepcyjnie to nie to samo.
- Zawyża kontrast, gdy oba kolory są ciemne — przez to jest zawodny w dark mode.

## WCAG 3 i APCA — stan na październik 2026

- 10 września 2026 W3C opublikowało kolejny Working Draft WCAG 3.0. W3C pisze, że WCAG 3 „does not deprecate WCAG 2”.
- Algorytm kontrastu w WCAG 3: „yet to be determined”. Wymagania kontrastu tekstu mają status *developing*.
- APCA była w pierwszym drafcie (styczeń 2021), ale usunięto ją z draftów WCAG 3 w 2023. Projekt APCA mówi, że jest „being evaluated”.
- Szacunki ukończenia WCAG 3 różnią się: od 2027 (najwcześniej) przez ~2029 do „raczej nie przed 2030”.

> **Status: Disputed** — wiele artykułów opisuje APCA jako „metodę WCAG 3”. Aktualny draft tego nie potwierdza. Adrian Roselli ostrzega przed ryzykiem prawnym przy porzuceniu kontrastu WCAG 2 na tej podstawie.

### Progi APCA (Lc)

APCA uwzględnia rozmiar, wagę fontu i polaryzację (ciemne na jasnym vs jasne na ciemnym). Progi wg CSS DNA (2026):

| Zastosowanie | Lc |
|---|---|
| Mały/cienki tekst (~14–16px, waga 400) — zalecane | 90 |
| Zwykły tekst — minimum (18px/400 lub 16px/500+) | 75 |
| Duży lub pogrubiony tekst | 60 |
| Bardzo duże nagłówki (36px/400 lub 24px/700), ikony, ramki, focus ring | 45 |
| Placeholder, disabled — nigdy tekst główny | 30 |
| Brak kontrastu | 15 |

Przykład różnicy: `#767676` na `#FFFFFF` ma ok. 4.54:1 (przechodzi AA), ale Lc 71.6 (poniżej Lc 75). `#6e6e6e` daje 5.10:1 i Lc 75.

## OKLCH — budowa palety

- OKLCH = jasność (L), chroma (C), odcień (H). Jasność jest percepcyjnie równa, więc kroki skali wyglądają równo, a zmiana odcienia nie psuje kontrastu tak jak w HSL.
- Tailwind v4 i shadcn/ui używają OKLCH domyślnie. Przykład skali: `--color-brand-50: oklch(98% 0.01 250)` … `--color-brand-500: oklch(60% 0.16 250)` … `--color-brand-950: oklch(12% 0.06 250)`.
- Dark mode: ten sam odcień, wyższa jasność dla akcentu, np. jasny motyw `oklch(0.62 0.19 256)`, ciemny `oklch(0.72 0.19 256)`.
- Refactoring UI: na kolorowym tle zamiast szarego tekstu użyj odcienia bliskiego kolorowi tła.

## Jak stosować

- [ ] Cel zgodności: WCAG 2.2 AA (4.5:1 tekst, 3:1 duży tekst i UI).
- [ ] Nowa paleta: sprawdź oba modele — WCAG 2 i APCA.
- [ ] Dark mode: polegaj bardziej na APCA, bo WCAG 2 zawodzi przy jasnym na ciemnym.
- [ ] Testuj kolory faktycznie wyrenderowane (przezroczystości, nakładki), nie tylko wartości w CSS.
- [ ] Przy APCA kolejność ma znaczenie: tekst vs tło to nie to samo co tło vs tekst.
- [ ] Szary tekst drugorzędny: sprawdź, czy nie spadł poniżej 4.5:1 — to najczęstszy błąd.
- [ ] Placeholder i disabled mogą mieć niższy kontrast, ale nigdy treść.
- [ ] Palety definiuj w OKLCH i trzymaj w tokenach — [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md).

Fragment promptu dla agenta:

```
All text must meet WCAG 2.2 AA (4.5:1 normal, 3:1 large text and UI components).
Additionally aim for APCA Lc 75+ for body text. Define colors in OKLCH as
semantic tokens (background/foreground, primary/primary-foreground, muted...).
Verify contrast for both light and dark themes.
```

## Zobacz też

- [Podstawy web designu dla developera](web-design-fundamentals.md) — hierarchia przez kolor i wagę
- [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md) — semantyczne tokeny kolorów

---
title: Podstawy web designu dla developera
updated: 2026-10-28
tags: [web-design, hierarchy, spacing, typography, layout, responsive]
sources:
  - "[Refactoring UI](https://refactoringui.com/) — 2018 — high"
  - "[Refactoring UI · notatki](https://mutto.fyi/books/refactoring-ui/) — unknown — medium"
  - "[Refactoring UI — podsumowanie](https://sobrief.com/books/refactoring-ui) — unknown — medium"
  - "[What Is the 8-Point Grid System in UI Design?](https://wpdean.com/what-is-the-8-point-grid-system/) — unknown — low"
  - "[UI Grids: The Complete Guide (2026)](https://www.uxpin.com/studio/blog/ui-grids-how-to-guide/) — 2026 — medium"
  - "[Utopia — fluid type & space calculator](https://utopia.fyi/) — unknown — high"
  - "[Reimagining Fluid Typography (OddBird)](https://www.oddbird.net/2025/02/12/fluid-type/) — 2025-02-12 — high"
  - "[Container queries in 2026 (LogRocket)](https://blog.logrocket.com/container-queries-2026/) — 2026 — medium"
  - "[How to Approach Responsive Web Development (Geary.co)](https://geary.co/responsive-development-era-4/) — 2025 — medium"
  - "[Responsive Web Design: A Complete Guide 2026 (Scrimba)](https://scrimba.com/articles/responsive-web-design-a-complete-guide-2026-2/) — 2026 — medium"
  - "[leonxlnx/taste-skill — SKILL.md (Laws of the craft)](https://github.com/leonxlnx/taste-skill/blob/main/skills/taste-skill/SKILL.md) — unknown — medium"
  - "[pbakaus/impeccable — reference/craft-floor.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/craft-floor.md) — unknown — high"
---

# Podstawy web designu dla developera

> Interfejs wygląda dobrze głównie dzięki hierarchii: ważne rzeczy dominują, reszta jest wyciszona.
> Hierarchię budujesz wagą fontu i kolorem, nie tylko rozmiarem. Odstępy bierzesz ze stałej skali (8px, z 4px na drobne korekty).
> Typografię i odstępy skalujesz płynnie przez `clamp()`. Layout ma być najpierw „sam z siebie” elastyczny, potem container queries, na końcu media queries.

## Hierarchia wizualna

Główna teza Refactoring UI (Adam Wathan, Steve Schoger): największy wpływ na „dobry wygląd” ma hierarchia, nie ozdobniki. Rozdział nazywa się „Not all elements are equal”.

- **Nie wszystko jest równie ważne.** Gdy wszystko walczy o uwagę, powstaje „ściana treści”.
- **Rozmiar to nie wszystko.** Hierarchia oparta tylko na rozmiarze daje za duże nagłówki i za mały tekst drugorzędny. Używaj wagi i koloru.
- **Trzy kolory tekstu:** ciemny (główny), szary (drugorzędny), jaśniejszy szary (trzeciorzędny).
- **Dwie wagi:** normalna 400–500 i pogrubiona 600–700. W UI unikaj wag poniżej 400.
- **Wyciszaj, żeby wyróżnić.** Zamiast podbijać ważny element, przygaś to, co z nim konkuruje (typowo: nawigacja).
- **Etykiety to ostateczność.** Format „etykieta: wartość” daje wszystkiemu równą wagę. Jeśli etykieta musi być — mniejsza, słabszy kontrast.
- **Szary tekst nie na kolorowym tle.** Na kolorowym tle zbliż kolor tekstu do koloru tła zamiast dawać szary.
- **Hierarchia wizualna ≠ hierarchia dokumentu.** `h1` nie musi być największy na ekranie. Semantyka HTML i wygląd to dwie osobne decyzje.
- **Balansuj wagę i kontrast.** Ciężką ikonę uspokaja niższy kontrast, cienkiej ramce pomaga większa grubość.

## Odstępy i siatka

- **Skala 8px jako domyślna:** odstępy, paddingi i marginesy to wielokrotności 8 (8, 16, 24, 32…). Pół kroku (4px) na ciasne miejsca, np. ikona–etykieta.
- **Bliskość buduje grupy (Gestalt):** wewnątrz grupy mały odstęp (8–16px), między grupami duży (24–32px i więcej). Przykład formularza: etykieta–pole 4–8px, grupa–grupa 16–24px.
- **Siatka sama nie tworzy hierarchii.** Interfejs może idealnie trzymać się 8pt i dalej być nieczytelny, jeśli kontrast typografii i punkty skupienia są źle ustawione.
- **Gutter:** 16–24px dla większości layoutów, 24–32px dla przestronnych stron redakcyjnych, 12–16px dla gęstych interfejsów z danymi.
- Refactoring UI radzi zaczynać od **za dużej** ilości białej przestrzeni i ją zmniejszać.

## Typografia

- **Skala modularna:** rozmiary fontów z jednego współczynnika (np. 1.2 na mobile, 1.333 na desktop), a nie losowe wartości.
- **Płynna skala (Utopia):** definiujesz bazowy rozmiar i współczynnik na dwóch szerokościach ekranu (np. 320px i 1500px). Narzędzie generuje `clamp()` dla każdego kroku. Konwencja nazw: `--step--2` … `--step-5` dla fontów, `--space-3xs` … `--space-3xl` dla odstępów.
  - Przykład: `--step-0: clamp(1rem, 0.9286rem + 0.3571vi, 1.25rem);`
  - Nagłówki mapujesz na kroki: `h1` → `var(--step-5)`, tekst → `var(--step-0)`.
- **Ten sam mechanizm dla odstępów.** Płynne fonty plus płynne odstępy dają proporcje spójne na każdej szerokości, nie tylko w breakpointach.
- **Dostępność płynnych fontów (OddBird, 2025):** typowy `clamp(1.125rem, ... vi, 1.25rem)` zawsze daje rozmiar większy niż ustawił użytkownik. Proponowana alternatywa: clamp oparty na `em` na elemencie `html`, np. `clamp(1em, 0.9em + 1vw, 1.5em)`.
- Coraz częściej używa się jednostek `vi` (inline) zamiast `vw` oraz `cqi` (względem kontenera).

## Liczby ze stron nagradzanych (taste-skill)

Autorzy `taste-skill` podają te liczby z analizy 247 stron z galerii One Page Love i Awwwards. Część reguł to ich własny styl, oznaczony w źródle jako „house style”.

- **Typografia:**
  - Widoczną pracę robią 2–3 rozmiary: jeden bardzo duży, jeden mały. Mediana stosunku nagłówka do tekstu to 4.3. Najlepsze strony mają największy tekst o medianie 8.4vw, słabe 5.0vw.
  - Display: tracking od -0.02 do -0.05em, interlinia 0.85–1.05.
  - Tekst: 16–20px, interlinia 1.45–1.6, 45–75 znaków w linii.
  - Najwyżej 5 rozmiarów na stronie. Jedna rodzina kroju to norma (około jedna trzecia stron), dwie to limit.
  - Domyślnie wyrównanie do lewej. Wyśrodkuj najwyżej jeden moment.
- **Przestrzeń:**
  - Jedna siatka i jedna para wąskich marginesów (16–32px). Duże elementy biegną do krawędzi.
  - Bloki tekstu mają na całej stronie 2–3 wspólne lewe krawędzie.
  - Odstęp między sekcjami 120–240px na desktopie (mediana około 240). Musi być wyraźnie większy niż każdy odstęp wewnątrz sekcji.
  - Sąsiednie sekcje mają różne kompozycje.
- **Przyciski:** płaskie, jeden kolor, albo kwadratowe, albo w pełni zaokrąglone (52% i 23% najlepszych stron). Zaokrąglenie 9–16px to domyślny wybór słabych stron.
- **Impeccable:** więcej miejsca nad nagłówkiem niż pod nim. Display maksymalnie 6rem, tracking nie niżej niż -0.04em.

> **Status: Disputed** — Refactoring UI (wyżej) buduje hierarchię kolorem: do 3 kolorów tekstu, w tym szary drugorzędny. `taste-skill`: „Running text in the full ink. A page set in soft grey reads unfinished.” `impeccable`: na kolorowym tle barw drugorzędny tekst od barwy tła, „never gray”. Zgoda co do jednego: tekst ciągły nie może być bladoszary. Szarość zostaw dla metadanych i etykiet, przy zachowanym kontraście.

## Layout i responsywność w 2026

Kolejność podejść (Geary.co):
1. **Responsywność wewnętrzna (intrinsic)** — elementy dopasowują się same, bez zapytań: `grid` z `auto-fit`/`minmax()`, `flex-wrap`, `clamp()`.
2. **Responsywność względem dostępnego miejsca** — gdy zachowanie zależy od rodzica, użyj container queries.
3. **Responsywność względem urządzenia** — media queries tylko gdy 1 i 2 nie wystarczą (struktura całej strony).

Container queries:
- Wzorzec: rodzic `container-type: inline-size`, dzieci w `@container (min-width: …)`. Jednostki `cqi`/`cqb`/`cqw` liczą się względem kontenera.
- Zapytania o rozmiar (size queries) mają szerokie wsparcie przeglądarek. Style queries — częściowe. Scroll-state queries — ograniczone.
- LogRocket: media queries same nie rozwiążą komponentu, którego szerokość nie zależy od viewportu — to argument za container queries. Uwaga na pułapki, np. zapadanie się treści we flexboxie.

Scrimba (2026) podsumowuje zestaw: media queries dla struktury strony, container queries dla komponentów, `clamp()` dla płynnej typografii, intrinsic Grid dla layoutu bez breakpointów.

## Jak stosować

Checklista przed oddaniem ekranu (także do promptu dla LLM):

- [ ] Na ekranie jest jeden wyraźny punkt skupienia. Reszta jest wyciszona.
- [ ] Tekst ma maksymalnie 3 kolory i 2 wagi. Brak wag < 400.
- [ ] Hierarchia robiona wagą i kolorem, nie tylko rozmiarem.
- [ ] Wszystkie odstępy pochodzą ze skali (4/8/16/24/32/48/64…). Brak „magicznych” wartości.
- [ ] Odstęp wewnątrz grupy < odstęp między grupami.
- [ ] Rozmiary fontów pochodzą ze skali modularnej (najlepiej płynnej, z Utopii).
- [ ] Layout działa bez media queries tam, gdzie się da (`auto-fit`, `minmax`, `flex-wrap`).
- [ ] Komponenty wielokrotnego użytku reagują na kontener (`@container`), nie na viewport.
- [ ] Kontrast tekstu sprawdzony — patrz [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md).
- [ ] Wartości są w tokenach, nie wpisane na sztywno — patrz [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md).

Fragment promptu dla agenta:

```
Use an 8px spacing scale (4px only for tight inner gaps). Max 3 text colors
(primary, secondary, tertiary) and 2 font weights (400, 600). Build hierarchy
with weight and color before size. Group related items with smaller gaps than
gaps between groups. Prefer intrinsic layout (grid auto-fit/minmax), then
container queries for components, media queries only for page structure.
```

## Zobacz też

- [Kolor i kontrast — OKLCH, WCAG 2, APCA](color-and-contrast.md) — kolory, kontrast, WCAG i APCA
- [Design tokens — DTCG, Tailwind v4, shadcn/ui](design-tokens.md) — jak zamknąć skale w tokenach
- [DESIGN.md — design system w jednym pliku dla agenta](design-md.md) — jak przekazać te zasady agentowi w jednym pliku
- [Przegląd designu — rubryki, punktacja, kolejność poprawek](design-review.md) — jak sprawdzić te zasady na zrzutach ekranu

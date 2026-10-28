---
title: Techniki SVG na web — viewBox, prymitywy, dostępność, animacja
updated: 2026-10-28
tags: [svg, web, accessibility, animation]
sources:
  - "Claude built-in skill artifact-diagramming (wbudowany skill Claude Code, Anthropic) — unknown — high"
  - "[Using ARIA to enhance SVG accessibility — TPGi](https://www.tpgi.com/using-aria-enhance-svg-accessibility/) — unknown — high"
  - "[SVG images accessibility — Orange digital accessibility guidelines](https://a11y-guidelines.orange.com/en/articles/accessible-svg/) — unknown — high"
  - "[Implementing Accessible SVG Elements — The A11Y Collective](https://www.a11y-collective.com/blog/svg-accessibility/) — unknown — medium"
  - "[How to Animate SVG: CSS, SMIL, WAAPI, and GSAP Compared — svg.dog](https://svg.dog/learn/how-to-animate-svg/) — unknown — medium"
  - "[SVG Animation in 2026: Capabilities, Trade-offs, and Best Practices — adsights.ai](https://www.adsights.ai/blog/topics/creative-strategy/svg-animation-capabilities-and-best-practices) — 2026 — low"
  - "[Using AI to Generate SVG Icons — allsvgicons.com](https://allsvgicons.com/blog/ai-generate-svg-icons-tools-workflows/) — unknown — low"
  - "[vercel-labs/web-interface-guidelines — command.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/command.md) — unknown — high"
  - "[pbakaus/impeccable — reference/craft-floor.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/craft-floor.md) — unknown — high"
---

# Techniki SVG na web — viewBox, prymitywy, dostępność, animacja

> Rozmiar ustawiaj przez `viewBox`, a skalowanie zostaw CSS. Kolory dawaj przez `currentColor`, żeby grafika działała w jasnym i ciemnym motywie. Buduj z prymitywów i nazwanych grup `<g>`. Grafika z treścią dostaje `role="img"` i nazwę, a dekoracyjna `aria-hidden="true"`. Animuj domyślnie przez CSS i zawsze obsłuż `prefers-reduced-motion`.

## viewBox i siatka

- Ustaw `viewBox="0 0 W H"` i skaluj przez CSS (`max-width: 100%; height: auto`). W i H dobierz do treści, nie do gotowego presetu (artifact-diagramming).
- Ikony: typowo `viewBox="0 0 24 24"`, obrys np. 2px, zaokrąglone końce. Sprawdzaj czytelność w 24 i 48 px (allsvgicons).
- Wyrównuj do siatki. Wspólne linie bazowe i równe odstępy sprawiają, że rysunek wygląda na celowy. Przesunięcia „na oko” wyglądają jak szum (artifact-diagramming).
- Przepływy rysuj od lewej do prawej, warstwy z góry na dół (artifact-diagramming).

## Prymitywy kontra ścieżki

- Prymitywy (`rect`, `circle`, `ellipse`, `line`, `polyline`, `polygon`) LLM liczy pewnie. Łatwo je też poprawić w kolejnej iteracji.
- `path` z krzywymi Béziera zostaw na końcowe detale. Szczegóły procesu w [Workflow generowania SVG przez LLM](svg-workflow-llm.md).
- Grupuj części w `<g id="nazwa">`. Kod da się wtedy czytać, edytować promptem i animować per część.
- Strzałki w diagramach rób przez `<marker>` w `<defs>` i `marker-end="url(#arrow)"` albo małym `<polygon>`. Nigdy obrazkiem (artifact-diagramming).

## Kolor i motywy

- Obrysy, tekst i groty strzałek w `currentColor` dziedziczą kolor tekstu strony w jasnym i ciemnym motywie (artifact-diagramming).
- Dosłowny kolor zostaw dla jednego elementu, który niesie znaczenie. Sprawdź, czy czyta się na obu tłach.

## Tekst w SVG

- Rozmiar mniej więcej 11–13 px w skali rysunku. Wyrównanie przez `text-anchor`. Krótkie etykiety, od jednego do trzech słów (artifact-diagramming).
- Dłuższe wyjaśnienia dawaj w `<figcaption>` pod rysunkiem, nie w samej grafice.

## Samowystarczalne SVG

- Bez `<script>`, `<style>` i `<foreignObject>` w środku. Gradienty, wzory i `<use>` odwołują się do id w tym samym pliku (`href="#id"`) (artifact-diagramming).
- Ta zasada pochodzi z wytycznych do diagramów w artefaktach. W zwykłym projekcie web `<style>` w SVG jest dozwolony. Ułatwia np. animację CSS w pliku ładowanym jako `<img>`.

## Dostępność

- Grafika z treścią, wzorzec najpewniejszy:

```html
<svg role="img" aria-labelledby="t1 d1" viewBox="0 0 24 24">
  <title id="t1">Koszyk</title>
  <desc id="d1">Ikona koszyka z dwoma produktami</desc>
  ...
</svg>
```

- `<title>` jako pierwsze dziecko `<svg>`. Unikalne id, bo zduplikowane psują `aria-labelledby` (TPGi, A11Y Collective).
- Samo `<title>`/`<desc>` nie jest pewnie odczytywane przez czytniki ekranu. Dlatego dodaj ARIA (`aria-labelledby` lub `aria-label`) i `role="img"` (TPGi).
- `aria-label` i `<title>` naraz: wygrywa `aria-label`. Wybierz jedno.
- Krótka nazwa: `<svg role="img" aria-label="...">` (Orange).
- SVG w `<img>`: atrybut `alt` i `role="img"` (Orange).
- Grafika dekoracyjna: `aria-hidden="true"`, bez `title`/`desc` i bez innych atrybutów nazwy (Orange).
- Podstawa: WCAG 1.1.1 „Non-text Content”, poziom A.
- W diagramach: `<figure>` z `<figcaption>` mówiącym, co pokazuje rysunek, plus `aria-label` z tą samą treścią (artifact-diagramming).

## Ikony (impeccable craft-floor)

- Ikony mają być z prawdziwej biblioteki albo z własnego SVG, o jednej grubości kreski w całym zestawie. Znaki Unicode i emoji zamiast ikon to tik designu z AI.
- Geometryczna maska (koło, wielokąt, `clip-path` z wieloma wierzchołkami) udająca kontur zdjęcia wygląda gorzej niż brak efektu. Zrób maskę alfa z prawdziwego obrazu albo wycięty asset.

## Animacja

- **CSS**: domyślny wybór. Nie wymaga JS. Transformacje i `opacity` liczy GPU. Wyłączysz ją media query (svg.dog).
- **Web Animations API**: gdy potrzebujesz interakcji, przewijania osi czasu albo złożonej interpolacji (svg.dog).
- **Transformacje części SVG** (Vercel Web Interface Guidelines): dawaj je na grupę `<g>` z `transform-box: fill-box; transform-origin: center`. Inaczej obrót i skala liczą się względem całego płótna.
- **SMIL** (`<animate>`): tylko w wąskich przypadkach. CSS `prefers-reduced-motion` nie wyłącza SMIL. Trzeba to zrobić w JS.

> **Status: Disputed** — stan SMIL. Jedno źródło pisze, że wsparcie jest niespójne i nie zaleca go do nowych projektów. Inne pisze, że wszystkie nowoczesne przeglądarki go obsługują (podsumowanie wyszukiwania; svg.dog, effect-labs).

- Reduced motion w CSS:

```css
@media (prefers-reduced-motion: reduce) {
  svg * { animation: none !important; }
  .line-draw { stroke-dashoffset: 0; } /* pokaż gotowy rysunek zamiast pustej ścieżki */
}
```

- SVG ładowane jako `<img>` lub `background-image` nie sprawdza `prefers-reduced-motion` ze strony. Wtedy wstaw SVG inline albo podmień plik na statyczny przez media query na stronie (adsights.ai).
- Nie przekazuj informacji samym ruchem. Daj możliwość pauzy (adsights.ai).

## Jak stosować

Checklista przed oddaniem SVG:
- [ ] `viewBox` ustawiony, brak sztywnych `width`/`height` albo skalowanie przez CSS.
- [ ] Kolory przez `currentColor` (poza jednym akcentem).
- [ ] Części w nazwanych `<g>`. Prymitywy tam, gdzie się da.
- [ ] Treść: `role="img"` + `aria-labelledby` lub `aria-label`. Dekoracja: `aria-hidden="true"`.
- [ ] Animacja w CSS z obsługą `prefers-reduced-motion`.
- [ ] Przepuszczone przez SVGO (patrz [Narzędzia SVG — render, optymalizacja, modele i benchmarki](svg-tools.md)).

## Zobacz też
- [Workflow generowania SVG przez LLM](svg-workflow-llm.md) — proces: plan, prymitywy, render, poprawka
- [Narzędzia SVG — render, optymalizacja, modele i benchmarki](svg-tools.md) — render do PNG, SVGO, modele SVG
